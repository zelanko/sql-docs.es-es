---
title: Administrar SQL Server en Linux con SSMS | Documentos de Microsoft
description: Este tutorial muestra cómo usar SQL Server Management Studio en Windows para conectarse a SQL Server ejecutando en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 30cc4564-f389-4707-9b25-8ba782cc5150
ms.openlocfilehash: 95f97fdb3b35d50e671f9569a8b58315014fc509
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="use-sql-server-management-studio-ssms-on-windows-to-manage-sql-server-on-linux"></a>Usar SQL Server Management Studio (SSMS) de Windows para administrar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo muestra cómo usar [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) para conectarse a SQL Server 2017 en Linux. SSMS es una aplicación de Windows, así que usa SSMS cuando tiene una máquina de Windows que se puede conectar a una instancia remota de SQL Server en Linux.

Después de conectarse correctamente, ejecute una consulta de Transact-SQL (T-SQL) simple para comprobar la comunicación con la base de datos.

## <a name="install-the-newest-version-of-sql-server-management-studio"></a>Instale la versión más reciente de SQL Server Management Studio

Al trabajar con SQL Server, debe utilizar siempre la versión más reciente de SQL Server Management Studio (SSMS). La versión más reciente de SSMS se actualiza continuamente y optimizado y funciona con SQL Server actualmente Linux de 2017. Para descargar e instalar la versión más reciente, consulte [descargar SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para mantenerse al día, la versión más reciente de SSMS le avisa cuando hay una nueva versión disponible para su descarga. 

## <a name="connect-to-sql-server-on-linux"></a>Conectarse a SQL Server en Linux

Los pasos siguientes muestran cómo conectarse a SQL Server 2017 en Linux con SSMS.

1. Inicie SSMS escribiendo **Microsoft SQL Server Management Studio** en las ventanas del cuadro de búsqueda y, a continuación, haga clic en la aplicación de escritorio.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png)

2. En el **conectar al servidor** ventana, escriba la información siguiente (si SSMS ya se está ejecutando, haga clic en **conectar > motor de base de datos** para abrir el **conectar al servidor** ventana):

   | Configuración | Description |
   |-----|-----|
   | **Tipo de servidor** | El valor predeterminado es el motor de base de datos; No cambie este valor. |
   | **Nombre del servidor** | Escriba el nombre de la máquina de SQL Server de Linux de destino o su dirección IP. |
   | **Autenticación** | Para SQL Server de 2017 en Linux, use **autenticación de SQL Server**. |
   | **Inicio de sesión** | Escriba el nombre de un usuario con acceso a una base de datos en el servidor (por ejemplo, el valor predeterminado **SA** cuenta creada durante la instalación). |
   | **Contraseña** | Escriba la contraseña para el usuario especificado (para el **SA** cuenta, creó esto durante la instalación). |

    ![SQL Server Management Studio: Conectarse al servidor de base de datos SQL](./media/sql-server-linux-develop-use-ssms/connect.png)

3. Haga clic en **Conectar**.

    > [!TIP]
    > Si recibe un error de conexión, intente primero diagnosticar el problema a partir del mensaje de error. Luego revise las [recomendaciones para solucionar problemas de conexión](sql-server-linux-troubleshooting-guide.md#connection).
 
5. Después de conectarse correctamente a su servidor de SQL, **Explorador de objetos** se abre y ahora puede acceder a la base de datos para realizar tareas administrativas o consultar los datos.
 
     ![Explorador de objetos](./media/sql-server-linux-develop-use-ssms/object-explorer.png)
     
## <a name="run-sample-queries"></a>Ejecutar consultas de ejemplo

Después de conectarse al servidor, puede conectarse a una base de datos y ejecutar una consulta de ejemplo. Si está familiarizado con la escritura de consultas, vea [escribir instrucciones Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Identificar a la utilice para ejecutar una consulta en una base de datos. Podría tratarse de una base de datos que creó en el [tutorial de Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md). O bien podría estar el **AdventureWorks** ejemplo la base de datos que [descargar y restaurar](sql-server-linux-migrate-restore-database.md).
2. En **Explorador de objetos**, vaya a la base de datos de destino en el servidor.
2. Haga clic en la base de datos y, a continuación, seleccione **nueva consulta**:

    ![Nueva consulta. Conectarse al servidor de base de datos SQL: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/new-query.png)

3. En la ventana de consulta, escribir una consulta de Transact-SQL para seleccionar datos de una de las tablas. En el ejemplo siguiente se seleccionan datos de la **Production.Product** tabla de la **AdventureWorks** base de datos.

        SELECT TOP 10 Name, ProductNumber
        FROM Production.Product
        ORDER BY Name ASC

4. Haga clic en el **Execute** botón:

    ![Correcto. Conectarse al servidor de base de datos SQL: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/execute-query.png)

## <a name="next-steps"></a>Pasos siguientes

Además de las consultas, puede usar instrucciones T-SQL para crear y administrar las bases de datos.

Si está familiarizado con T-SQL, vea [Tutorial: escribir instrucciones de Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md) y [referencia de Transact-SQL (motor de base de datos)](https://msdn.microsoft.com/library/bb510741.aspx).

Para obtener más información sobre cómo usar SSMS, vea [usar SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
