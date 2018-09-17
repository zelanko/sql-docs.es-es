---
title: Conexión a orígenes de datos y a recursos compartidos de archivos con la autenticación de Windows | Microsoft Docs
description: Aprenda a configurar el catálogo de SSIS en Azure SQL Database y Azure-SSIS Integration Runtime para ejecutar paquetes que se conectar a orígenes de datos y recursos compartidos de archivos con la autenticación de Windows.
ms.date: 06/27/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 8979512a2ac2edeba8a5a6479fe0ef8bb6c3179a
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2018
ms.locfileid: "45564011"
---
# <a name="connect-to-data-sources-and-file-shares-with-windows-authentication-from-ssis-packages-in-azure"></a>Conexión a orígenes de datos y a recursos compartidos de archivos con la autenticación de Windows de paquetes SSIS en Azure
Puede usar la autenticación de Windows para conectarse a orígenes de datos y recursos compartidos de archivos que están en la misma red virtual que Azure SSIS Integration Runtime (IR), tanto en máquinas virtuales locales o de Azure como en Azure Files. Hay tres métodos para conectarse a orígenes de datos y recursos compartidos de archivos con la autenticación de Windows de paquetes SSIS que se ejecutan en Azure-SSIS IR:

| Método de conexión | Ámbito efectivo | Paso de configuración | Método de acceso en paquetes | Número de conjuntos de credenciales y recursos conectados | Tipo de recursos conectados | 
|---|---|---|---|---|---|
| Credenciales persistentes a través del comando `cmdkey` | Por Azure-SSIS IR | Ejecute el comando `cmdkey` en un script de instalación personalizada (`main.cmd`) al aprovisionar o volver a configurar Azure-SSIS IR, por ejemplo, `cmdkey /add:fileshareserver /user:xxx /pass:yyy`.<br/><br/> Para obtener más información, consulte [Instalación personalizada del entorno de ejecución para la integración de SSIS en Azure](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup). | Acceda a los recursos directamente en los paquetes a través de la ruta de acceso UNC, por ejemplo, `\\fileshareserver\folder` | Compatibilidad con varios conjuntos de credenciales para los distintos recursos conectados | - Recursos compartidos de archivos en las máquinas virtuales de Azure o locales<br/><br/> - Azure Files, consulte [Montaje de un recurso compartido de archivos de Azure y acceso al recurso compartido en Windows](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server con autenticación de Windows<br/><br/> - Otros recursos con autenticación de Windows |
| Configuración de un contexto de ejecución a nivel de catálogo | Por Azure-SSIS IR | Ejecute el procedimiento almacenado `catalog.set_execution_credential` de SSISDB para establecer un contexto de "ejecución como".<br/><br/> Para obtener más información, vea el resto de este artículo a continuación. | Acceso a los recursos directamente en paquetes | Compatibilidad con solo un conjunto de credenciales para todos los recursos conectados | - Recursos compartidos de archivos en las máquinas virtuales de Azure o locales<br/><br/> - Azure Files, consulte [Montaje de un recurso compartido de archivos de Azure y acceso al recurso compartido en Windows](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server con autenticación de Windows<br/><br/> - Otros recursos con autenticación de Windows | 
| Montaje de unidades en tiempo de ejecución del paquete (no persistencia) | Por paquete | Execute el comando `net use` en la tarea Ejecutar proceso que se agrega al principio del flujo de control en los paquetes, por ejemplo, `net use D: \\fileshareserver\sharename` | Acceso a recursos compartidos de archivos a través de las unidades asignadas | Compatibilidad con varias unidades para diferentes recursos compartidos de archivos | - Recursos compartidos de archivos en las máquinas virtuales de Azure o locales<br/><br/> - Azure Files, consulte [Montaje de un recurso compartido de archivos de Azure y acceso al recurso compartido en Windows](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) |
|||||||

> [!WARNING]
> Si no utiliza ninguno de los métodos anteriores para conectarse a orígenes de datos y recursos compartidos de archivos con autenticación de Windows, los paquetes que dependen de la autenticación de Windows no podrán conectarse a estos y se producirá un error en tiempo de ejecución. 

En el resto de este artículo se describe cómo configurar el catálogo de SSIS en Azure SQL Database para ejecutar paquetes que usan la autenticación de Windows para conectarse a orígenes de datos y a recursos compartidos de archivos. 

## <a name="you-can-only-use-one-set-of-credentials"></a>Solo se puede usar un conjunto de credenciales
En este método, solo se puede usar un conjunto de credenciales en un paquete. Las credenciales de dominio que proporcione al seguir los pasos descritos en este artículo se aplican a todas las ejecuciones de paquetes, tanto interactivas como programadas, en la instancia de Azure-SSIS IR hasta que cambie o quite esas credenciales. Si el paquete tiene que conectarse a varios orígenes de datos y recursos compartidos de archivos con diferentes conjuntos de credenciales, es posible que considerar los métodos alternativos anteriores.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Proporcionar credenciales de dominio de autenticación de Windows
Para proporcionar las credenciales de dominio que permiten que los paquetes usen la autenticación de Windows para conectarse a orígenes de datos/recursos compartidos de archivos locales, realice lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB). Para más información, vea [Conectarse al catálogo de SSIS (SSISDB) en Azure](ssis-azure-connect-to-catalog-database.md).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado y proporcione las credenciales de dominio adecuadas:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Ejecute los paquetes de SSIS. Los paquetes usan las credenciales que proporcionó para conectarse a los orígenes de datos/recursos compartidos de archivos locales mediante la autenticación de Windows.

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
3.  Para conectarse con la autenticación de Windows, asegúrese de que Azure-SSIS IR pertenece a una red virtual que también incluye la instancia local de SQL Server.  Para obtener más información, consulte [Unión de una instancia de Integration Runtime de SSIS de Azure a una red virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Luego, use `catalog.set_execution_credential` para proporcionar las credenciales, como se describe en este artículo.

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
- Programar un paquete. Para más información, vea [Programar paquetes SSIS en Azure](ssis-azure-schedule-packages.md).