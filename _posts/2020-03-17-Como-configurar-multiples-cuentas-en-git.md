---
published: true
title: Cómo configurar múltiples cuentas en GIT
layout: post
license: ccby
tsocurl: https://thescienceofcode.azurewebsites.net/Articles/Show/5e71a2076dc6a240f8dbe934
---
![Cómo configurar múltiples cuentas en GIT]({{ site.baseurl }}/images/github-gitlab-ssh.png)

Vamos a explicar cómo configurar nuestra máquina para poder acceder a varios repositorios Git, usando diferentes credenciales entre ellos, sin necesidad de estar cambiando constantemente de cuentas.

<!--more-->

La guía aplica tanto para *Windows* como para *Linux* y no tiene límites en la cantidad de cuentas por proveedor. Si usas [Github Desktop](https://desktop.github.com/), [puedes ver estas guías](https://github.com/desktop/desktop/tree/development/docs/integrations) que son más sencillas.

> Puedes tener una cuenta configurada normalmente y usar este método para añadir las demás. Por ejemplo, si usas Github y ya lo tienes configurado, sólo debes seguir este procedimiento para las cuentas adicionales que vayas a incluír.

## Instrucciones

1. Tener instalado [GIT](https://git-scm.com/) en nuestra máquina.

2. Abrir *Git Bash* (en Windows se encuentra en el menú inicio luego de instalar GIT), en Linux podemos usar la línea de comandos por defecto.

3. Ir a la siguiente ubicación. En caso de que la carpeta *.ssh* no exista, crearla.
  
   ```bash
   # Windows 
   C:\NOMBRE_DE_USUARIO\.ssh

   # Linux
   ~/.ssh
   ```

4. Crear una nueva key ssh. **Importante**: Cuando el comando ejecutado pida un *passphrase*, como se supone que estás en un computador de confianza, puedes dar ENTER y dejar la llave sin *passphrase*, de esta forma te ahorrarás tener que estarla ingresando constantemente (o en su defecto tener que configurar el *ssh-agent*).

   ```bash
   # Windows 
   ssh-keygen.exe
   # Cuando pregunte por el filename, por ejemplo:
   file name: id_rsa_gitlab   
   
   # Linux
   ~/.ssh-keygen -t rsa -b 4096
   # Seguir instrucciones de igual forma que con Windows.
   ```

   > Para el nombre del archivo, es recomendable usar algo descriptivo como: *id_rsa_**PROVEEDOR**_**CUENTA***, donde los proveedores pueden ser github, gitlab, azurerepos, etc. Y la cuenta deberías usarlo sólo en caso de tener más de una por proveedor. Por ejemplo: *id_rsa_github*, *id_rsa_gitlab*, *id_rsa_github_work*, *id_rsa_gitlab_work*, etc.

5. Se crearán dos archivos, uno de ellos con extensión *.pub* (de public), abre el archivo y copia todo su contenido para agregar la clave al proveedor respectivo:

   * En general los pasos deberían ser: ser buscar en la configuración del proveedor, pegar la llave y guardar.

   * [Añadir una clave SSH en Github](https://help.github.com/es/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

   * [Añadir una clave SSH en Gitlab](https://www.tutorialspoint.com/gitlab/gitlab_ssh_key_setup.htm) - Sigue las instrucciones a partir del paso 2.

   * [Añadir una clave SSH en Azure Repos](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops&tabs=current-page) - Sigue las instrucciones a partir del paso 2.

   * [Añadir una clave SSH en Bitbucket](https://confluence.atlassian.com/bitbucketserver/ssh-user-keys-for-personal-use-776639793.html) - Sigue las instrucciones a partir del paso 2.

6. A continuación vamos a crear un archivo llamado **config** en la carpeta *.ssh* donde creamos las llaves anteriormente. El contenido del archivo podría ser un fragmento del siguiente (copia y personaliza sólo la parte que necesites, puedes tener tantas como quieras):

   ```bash

   # Github
   Host github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_github

   # Gitlab
   Host gitlab.com
   HostName gitlab.com
   User git
   IdentityFile ~/.ssh/id_rsa_gitlab

   # Azure repos
   Host ssh.dev.azure.com
   HostName ssh.dev.azure.com
   IdentityFile ~/.ssh/id_rsa_azurepos
   # Reemplaza con tu cuenta
   User your_msft@account.com
   IdentitiesOnly yes

   # Bitbucket
   Host bitbucket.org
   HostName bitbucket.org
   User git
   IdentityFile ~/.ssh/id_rsa_bitbucket

   # En caso de tener múltiples cuentas por proveedor
   # Por ejemplo:

   # Github work
   Host github.com-work
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_github_work
   ```

7. Clona el proyecto abriendo la URL del repo y escogiendo la opción SSH. Ten en cuenta lo siguiente:

   * Si sólo tienes una cuenta de ese proveedor:

      ```bash
      git clone URL_SSH

      # Ejemplo
      git clone git@github.com:equilaterus/wikilaterus.git
      ```

   * Si tienes varias cuentas por proveedor, asegúrate de usar el *Host* correcto:

      ```bash
      # Modifica el host!
      git clone URL_SSH_MODIFICADA

      # Ejemplo
      git clone git@github.com-work:equilaterus/wikilaterus.git
      ```

Luego de esto, podrás manipular tus repositorios normalmente, sin importar a qué cuenta pertenezcan. La ventaja, es que la configuración sólo debes hacerla una vez y de acuerdo al host que utlices durante el comando *git clone*, nuestro GIT sabrá que llaves utilizar para obtener acceso al repositorio.
