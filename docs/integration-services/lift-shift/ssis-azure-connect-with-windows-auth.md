---
title: "Conexión a orígenes de datos y a recursos compartidos de archivos con la autenticación de Windows | Microsoft Docs"
ms.date: 01/12/2018
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
ms.openlocfilehash: a8dc3c1f39ca65e9616372fee7995dfa41cd89a1
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows
En este artículo se describe cómo configurar el catálogo de SSIS en Azure SQL Database para ejecutar paquetes que usan la autenticación de Windows para conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure. Puede usar la autenticación de Windows para conectarse a orígenes de datos que están en la misma red virtual que Azure SSIS Integration Runtime, tanto de manera local como en las máquinas virtuales de Azure y en Azure Files.

> [!WARNING]
> Si no proporciona credenciales de dominio válidas para la Autenticación de Windows mediante la ejecución de `catalog`.`set_execution_credential`, tal y como se describe en este artículo, los paquetes que dependan de la Autenticación de Windows no podrán conectarse a los orígenes de datos y se producirá un error en tiempo de ejecución.

Las credenciales de dominio que proporcione al seguir los pasos descritos en este artículo se aplican a todas las ejecuciones de paquetes, tanto interactivas como programadas, en la instancia de SQL Database hasta que cambie o quite esas credenciales.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Proporcionar credenciales de dominio de autenticación de Windows
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

## <a name="connect-to-an-on-premises-sql-server"></a>Conectarse a un servidor SQL local
Para comprobar si puede conectarse a un servidor local de SQL Server, haga lo siguiente:

1.  Para ejecutar esta prueba, busque un equipo que no esté unido a ningún dominio.

2.  En el equipo que no esté unido a ningún dominio, ejecute el siguiente comando para iniciar SQL Server Management Studio (SSMS) con las credenciales de dominio que quiera usar:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  Desde SSMS, compruebe si puede conectarse al servidor local de SQL Server que quiere usar.

### <a name="prerequisites"></a>Prerequisites
Para conectarse a un servidor SQL local desde un paquete que se ejecuta en Azure, hay que habilitar los siguientes requisitos previos:

1.  En el Administrador de configuración de SQL Server, habilite el protocolo TCP/IP.
2.  Permita el acceso a través de Firewall de Windows. Para más información, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).
3.  Para conectarse con la autenticación de Windows, asegúrese de que Integration Runtime de SSIS de Azure pertenece a una red virtual (VNet) que también incluye el servidor SQL local.  Para obtener más información, consulte [Unión de una instancia de Integration Runtime de SSIS de Azure a una red virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Luego, use `catalog.set_execution_credential` para proporcionar las credenciales, como se describe en este artículo.

## <a name="connect-to-an-on-premises-file-share"></a>Conectarse a un recurso compartido de archivos local
Para comprobar si puede conectarse a un recurso compartido de archivos local, haga lo siguiente:

1.  Para ejecutar esta prueba, busque un equipo que no esté unido a ningún dominio.

2.  En el equipo que no está unido a ningún dominio, ejecute el siguiente comando. Este comando abre una ventana del símbolo del sistema con las credenciales de dominio que quiera usar y, seguidamente, obtiene un listado de directorios para probar la conectividad con el recurso compartido de archivos.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Compruebe si se devuelve la lista de directorios del recurso compartido de archivos local que quiere usar.

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>Conectarse a un recurso compartido de archivos en una máquina virtual de Azure
Haga lo siguiente para conectarse a un recurso compartido de archivos en una máquina virtual de Azure:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el procedimiento almacenado `catalog.set_execution_credential` tal como se describe en las siguientes opciones:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Conectarse a un recurso compartido de archivos en Azure Files
Para obtener más información acerca de Azure Files, consulte [Azure Files](https://azure.microsoft.com/services/storage/files/).

Haga lo siguiente para conectarse a un recurso compartido de archivos de Azure Files:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el procedimiento almacenado `catalog.set_execution_credential` tal como se describe en las siguientes opciones:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Pasos siguientes
- Implementar un paquete. Para obtener más información, consulte [Deploy an SSIS project with SQL Server Management Studio (SSMS) (Implementar un proyecto de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-deploy-ssms.md).
- Ejecutar un paquete. Para obtener más información, consulte [Run an SSIS package with SQL Server Management Studio (SSMS) (Ejecutar un paquete de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-run-ssms.md).
- Programar un paquete. Para obtener más información, consulte [Schedule SSIS package execution on Azure (Programar la ejecución de paquetes de SSIS en Azure)](ssis-azure-schedule-packages.md).
