---
title: 'Administrador de conexiones de Hadoop: SQL Server Integration Services | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 051fb627684e8a094ac0f39d5fffad9d9e399d0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841633"
---
# <a name="hadoop-connection-manager"></a>Administrador de conexiones de Hadoop
  El administrador de conexiones de Hadoop permite que un paquete de SQL Server Integration Services (SSIS) se conecte a un clúster de Hadoop usando los valores especificados para las propiedades.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Configuración del Administrador de conexiones de Hadoop  
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **Hadoop** > **Agregar**. Se abrirá el cuadro de diálogo **Hadoop Connection Manager Editor** (Editor del Administrador de conexiones de Hadoop).  
  
2.  Para configurar la información relacionada con el clúster de Hadoop, seleccione las pestañas **WebHCat** o **WebHDFS** en el panel izquierdo.
  
3.  Si habilita la opción **WebHCat** para invocar un trabajo de Pig o Hive en Hadoop, haga lo siguiente: 
  
    1.  En **Host de WebHCat**, especifique el servidor que hospeda el servicio WebHCat.  
  
    2.  Para **WebHCat Port**(Puerto de WebHCat), escriba el puerto del servicio WebHCat, cuyo valor predeterminado es 50111.  
  
    3.  Seleccione el método **Authentication** (Autenticación) para acceder al servicio WebHCat. Los valores disponibles son **Basic** (Básico) y **Kerberos**.  
  
         ![Captura de pantalla del editor del administrador de conexiones de Hadoop con autenticación básica](../../integration-services/connection-manager/media/hadoop-cm-basic.png "Editor del administrador de conexiones de Hadoop con autenticación básica")  
  
         ![Captura de pantalla del editor del administrador de conexiones de Hadoop con autenticación Kerberos](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Editor del administrador de conexiones de Hadoop con autenticación Kerberos")  
  
    4.  Para **WebHCat User**(Usuario de WebHCat), escriba el **usuario** autorizado para acceder a WebHCat.  
  
    5.  Si selecciona la autenticación **Kerberos** , escriba los valores **Password** (Contraseña) y **Domain**(Dominio) del usuario.  
  
4.  Si habilita la opción **WebHDFS** para copiar datos desde o en HDFS, haga lo siguiente: 
  
    1.  Para **WebHDFS Host**(Host de WebHDFS), especifique el servidor que hospeda el servicio WebHDFS.  
  
    2.  Para **WebHDFS Port**(Puerto de WebHDFS), escriba el puerto del servicio WebHDFS, cuyo valor predeterminado es 50070.  
  
    3.  Seleccione el método **Authentication** (Autenticación) para acceder al servicio WebHDFS. Los valores disponibles son **Basic** (Básico) y **Kerberos**.  
  
    4.  Para **WebHDFS User**(Usuario de WebHDFS), escriba el usuario autorizado para acceder a HDFS.  
  
    5.  Si selecciona la autenticación **Kerberos** , escriba los valores **Password** (Contraseña) y **Domain**(Dominio) del usuario.  
  
5.  Haga clic en **Probar conexión**. (Solo se prueba la conexión habilitada).  
  
6.  Seleccione **Aceptar** para cerrar el cuadro de diálogo.  

## <a name="connect-with-kerberos-authentication"></a>Conectar con la autenticación Kerberos
Hay dos opciones para configurar el entorno local de forma que pueda usar la autenticación Kerberos con el administrador de conexiones de Hadoop. Puede elegir la opción que mejor se adapte a sus circunstancias.
-   Opción 1: [unir el equipo SSIS al dominio Kerberos](#kerberos-join-realm)
-   Opción 2: [habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Opción 1: unir el equipo SSIS al dominio Kerberos

#### <a name="requirements"></a>Requisitos:

-   El equipo de puerta de enlace se debe unir al dominio Kerberos y no se puede unir a ningún dominio de Windows.

#### <a name="how-to-configure"></a>Cómo se configura:

En el equipo SSIS:

1.  Ejecute la utilidad **Ksetup** para configurar el dominio y el servidor de Centro de distribución de claves (KDC) de Kerberos.

    El equipo debe estar configurado como miembro de un grupo de trabajo, ya que un dominio Kerberos es diferente de un dominio de Windows. Establezca el dominio Kerberos y agregue un servidor KDC como se explica en el siguiente ejemplo. Reemplace `REALM.COM` por su dominio Kerberos propio correspondiente, según sea necesario.

    ```    
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    Después de ejecutar estos comandos, reinicie el equipo.

2.  Compruebe la configuración con el comando **Ksetup**. La salida debería ser similar a la del siguiente ejemplo:

    ```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="kerberos-mutual-trust"></a>Opción 2: habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos

#### <a name="requirements"></a>Requisitos:
-   El equipo de puerta de enlace se debe unir a un dominio de Windows.
-   Necesita permiso para actualizar la configuración del controlador de dominio.

#### <a name="how-to-configure"></a>Cómo se configura:

> [!NOTE]
> Reemplace `REALM.COM` y `AD.COM` en el siguiente tutorial por su dominio Kerberos y controlador de dominio propios correspondientes, según sea necesario.

En el servidor KDC:

1.  Edite la configuración del KDC en el archivo **krb5.conf**. Permita que KDC confíe en el dominio de Windows, haciendo referencia para ello a la siguiente plantilla de configuración. La configuración se encuentra de forma predeterminada en **/etc/krb5.conf**.

    ```
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    Reinicie el servicio KDC después de la configuración.

2.  Prepare una entidad de seguridad denominada  **krbtgt/REALM.COM@AD.COM** en el servidor KDC. Use el siguiente comando:

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  En el archivo de configuración del servicio de HDFS **hadoop.security.auth_to_local**, agregue `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

En el controlador de dominio:

1.  Ejecute los siguientes comandos **Ksetup** para agregar una entrada de dominio Kerberos:

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  Establezca una confianza entre el dominio de Windows y el dominio Kerberos. En el siguiente ejemplo, `[password]` es la contraseña de la entidad de seguridad **krbtgt/REALM.COM@AD.COM**.

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  Seleccione el algoritmo de cifrado que se va a usar con Kerberos.

    1. Vaya a **Administrador del servidor** > **Administración de directivas de grupo** > **Dominio**. Desde allí, vaya a **Objetos de directiva de grupo** > **Default or Active Domain Policy** (Directiva de dominio predeterminada o activa)  > **Editar**.

    2. En la ventana emergente del **Editor de administración de directivas de grupo**, vaya a **Configuración del equipo** > **Directivas** > **Configuración de Windows**. Desde allí, vaya a **Configuración de seguridad** > **Directivas locales** > **Opciones de seguridad**. Configure **Seguridad de red: configurar tipos de cifrado permitidos para Kerberos**.

    3. Seleccione el algoritmo de cifrado que quiere usar para conectarse al KDC. Normalmente, se puede seleccionar cualquiera de las opciones.

        ![Captura de pantalla de los tipos de cifrado de Kerberos](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. Use el comando **Ksetup** para especificar el algoritmo de cifrado que se usará en el dominio Kerberos específico.

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  Para usar la entidad de seguridad de Kerberos en el dominio de Windows, cree una asignación entre la cuenta de dominio y la entidad de seguridad de Kerberos.

    1. Vaya a **Herramientas administrativas** > **Equipos y usuarios de Active Directory**.

    2. Configure las características avanzadas; para ello, seleccione **Ver** > **Características avanzadas**.

    3. Busque la cuenta con la que quiera crear las asignaciones, haga clic con el botón derecho para ver **Asignaciones de nombres** y, después, seleccione la pestaña **Nombres Kerberos**.

    4. Agregue una entidad de seguridad del dominio Kerberos.

        ![Captura de pantalla del cuadro de diálogo Asignación de identidad de seguridad](media/hadoop-connection-manager/map-security-identity.png)

En el equipo de puerta de enlace:

Ejecute los siguientes comandos **Ksetup** para agregar una entrada de dominio Kerberos.

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

## <a name="see-also"></a>Vea también  
 [Tarea de Hive de Hadoop](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Tarea de Pig con Hadoop](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Tarea Sistema de archivos de Hadoop](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
