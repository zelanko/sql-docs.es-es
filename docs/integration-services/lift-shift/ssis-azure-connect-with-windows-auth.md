---
title: "Conectarse a orígenes de datos locales con autenticación de Windows | Documentos de Microsoft"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 25113093ccd068a9afe661e160ae3319025b7534
ms.contentlocale: es-es
ms.lasthandoff: 09/25/2017

---
# <a name="connect-to-on-premises-data-sources-with-windows-authentication"></a>Conectarse a orígenes de datos locales con autenticación de Windows
Este artículo describe cómo configurar el catálogo de SSIS en la base de datos de SQL de Azure para ejecutar paquetes que utilizan la autenticación de Windows para conectarse a orígenes de datos local.

Las credenciales de dominio que proporcione al seguir los pasos descritos en este artículo se aplican a todas las ejecuciones de paquetes en la instancia de base de datos SQL hasta que cambie o quite las credenciales.

## <a name="prerequisite"></a>Requisito previo
Antes de configurar las credenciales de dominio para la autenticación de Windows, compruebe si un equipo no unido a un dominio puede conectarse a los orígenes de datos locales en `runas` modo. Por ejemplo, para comprobar si puede conectarse a un servidor local de SQL, haga lo siguiente:

1.  Para ejecutar esta prueba, fFind en un equipo no unido al dominio.

2.  En el equipo no unido a un dominio, ejecute el siguiente comando para iniciar SQL Server Management Studio (SSMS) con las credenciales de dominio que desea usar:

   ```cmd
   runas.exe /netonly /user:<domain>\<username> SSMS.exe
   ```

3.  Desde SSMS, compruebe si puede conectarse al servidor SQL local que desea usar.

## <a name="provide-domain-credentials"></a>Proporcione las credenciales de dominio
Para proporcionar las credenciales de dominio que permiten paquetes usar autenticación de Windows para conectarse a orígenes de datos locales, realice lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL que hospede la base de datos de catálogo de SSIS (SSISDB). Para obtener más información, consulte [conectar a la base de datos de catálogo de SSISDB en Azure](ssis-azure-connect-to-catalog-database.md).

2.  Con SSISDB como la base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado y proporcione las credenciales de dominio adecuado:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  Ejecute los paquetes SSIS. Los paquetes utilizan las credenciales que proporcionó para conectarse a orígenes de datos locales con autenticación de Windows.

## <a name="view-domain-credentials"></a>Credenciales de dominio de vista
Para ver las credenciales de dominio de active, haga lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL que hospede la base de datos de catálogo de SSIS (SSISDB).

2.  Con SSISDB como la base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado y comprobar el resultado:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

## <a name="clear-domain-credentials"></a>Credenciales de dominio claro
Para borrar y eliminar las credenciales que proporcionó como se describe en este artículo, haga lo siguiente:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL que hospede la base de datos de catálogo de SSIS (SSISDB).

2.  Con SSISDB como la base de datos actual, abra una ventana de consulta.

3.  Ejecute el siguiente procedimiento almacenado:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="next-steps"></a>Pasos siguientes
- Implementar un paquete. Para obtener más información, consulte [implementar un proyecto de SSIS con SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Ejecutar un paquete. Para obtener más información, consulte [ejecutar un paquete SSIS con SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Programar un paquete. Para obtener más información, consulte [paquetes de SSIS de programación de ejecución en Azure](ssis-azure-schedule-packages.md)

