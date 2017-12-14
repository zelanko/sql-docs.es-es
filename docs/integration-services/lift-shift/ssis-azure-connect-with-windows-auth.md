---
title: "Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9235ffd3225e76ee94067519c72e997c451d9893
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows
En este artículo se describe cómo configurar el catálogo de SSIS en Azure SQL Database para ejecutar paquetes que usan la autenticación de Windows para conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure.

Las credenciales de dominio que proporcione al seguir los pasos descritos en este artículo se aplican a todas las ejecuciones de paquetes en la instancia de SQL Database hasta que cambie o quite esas credenciales.

## <a name="connect-to-on-premises-data-sources"></a>Conectarse a orígenes de datos locales

### <a name="prerequisite"></a>Requisito previo
Antes de configurar las credenciales de dominio de la autenticación de Windows, compruebe si un equipo que no esté unido a ningún dominio se puede conectar al origen de datos local en modo `runas`.

#### <a name="connecting-to-sql-server"></a>Conectarse a SQL Server
Para comprobar si puede conectarse a un servidor local de SQL Server, haga lo siguiente:

1.  Para ejecutar esta prueba, busque un equipo que no esté unido a ningún dominio.

2.  En el equipo que no esté unido a ningún dominio, ejecute el siguiente comando para iniciar SQL Server Management Studio (SSMS) con las credenciales de dominio que quiera usar:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  Desde SSMS, compruebe si puede conectarse al servidor local de SQL Server que quiere usar.

#### <a name="connecting-to-a-file-share"></a>Conectarse a un recurso compartido de archivos
Para comprobar si puede conectarse a un recurso compartido de archivos local, haga lo siguiente:

1.  Para ejecutar esta prueba, busque un equipo que no esté unido a ningún dominio.

2.  En el equipo que no está unido a ningún dominio, ejecute el siguiente comando. Este comando abre una ventana del símbolo del sistema con las credenciales de dominio que quiera usar y, seguidamente, obtiene un listado de directorios para probar la conectividad con el recurso compartido de archivos.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Compruebe si se devuelve la lista de directorios del recurso compartido de archivos local que quiere usar.

### <a name="provide-domain-credentials"></a>Proporcionar las credenciales de dominio
Para proporcionar las credenciales de dominio que permiten que los paquetes usen la autenticación de Windows para conectarse a orígenes de datos locales, realice lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB). Para obtener más información, consulte [Connect to the SSISDB Catalog database on Azure (Conectarse a la base de datos del catálogo de SSISDB en Azure)](ssis-azure-connect-to-catalog-database.md).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado y proporcione las credenciales de dominio adecuadas:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  Ejecute los paquetes de SSIS. Los paquetes usan las credenciales que proporcionó para conectarse a los orígenes de datos locales mediante la autenticación de Windows.

### <a name="view-domain-credentials"></a>Ver las credenciales de dominio
Para ver las credenciales de dominio activas, haga lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado y compruebe el resultado:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>Borrar las credenciales de dominio
Para borrar y eliminar las credenciales que proporcionó tal como se describe en este artículo, haga lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-file-shares"></a>Conectarse a recursos compartidos de archivos
Puede usar la autenticación de Windows para conectarse a recursos compartidos de archivos que estén en la misma red virtual que Azure SSIS Integration Runtime, tanto de manera local como en las máquinas virtuales de Azure y en Azure Files. Para obtener más información acerca de Azure Files, consulte [Azure Files](https://azure.microsoft.com/services/storage/files/).

Para conectarse a un recurso compartido de archivos en una máquina virtual o un recurso compartido de archivos de Azure, realice lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el procedimiento almacenado `catalog.set_execution_credential` tal como se describe en las siguientes opciones:

    a.  Para conectarse a un recurso compartido de archivos en una máquina virtual de Azure, ejecute el siguiente procedimiento almacenado:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

    b.  Para conectarse a un recurso compartido de archivos de Azure (es decir, Azure Files), ejecute el siguiente procedimiento almacenado:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Pasos siguientes
- Implementar un paquete. Para obtener más información, consulte [Deploy an SSIS project with SQL Server Management Studio (SSMS) (Implementar un proyecto de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-deploy-ssms.md).
- Ejecutar un paquete. Para obtener más información, consulte [Run an SSIS package with SQL Server Management Studio (SSMS) (Ejecutar un paquete de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-run-ssms.md).
- Programar un paquete. Para obtener más información, consulte [Schedule SSIS package execution on Azure (Programar la ejecución de paquetes de SSIS en Azure)](ssis-azure-schedule-packages.md).
