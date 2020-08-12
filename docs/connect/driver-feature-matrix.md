---
title: Matriz de compatibilidad de características del controlador
description: Obtenga información sobre las características populares que se admiten en los controladores para SQL Server y dónde encontrar información sobre ellas.
ms.custom: ''
ms.date: 06/17/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-daenge
ms.openlocfilehash: a879b3784b19de4e7d30e1af213953b8e592abf9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84947895"
---
# <a name="driver-feature-support-matrix-for-microsoft-sql-server"></a>Matriz de compatibilidad de características del controlador para Microsoft SQL Server

Si tiene previsto usar una característica en Microsoft SQL Server, es posible que no esté disponible en todos los controladores. Entre los motivos por los que una característica podría no estar en un controlador determinado se encuentran los siguientes:

- La característica no se aplica a la tecnología del controlador.
- La característica es nueva y aún no se ha implementado en todos los controladores.
- La característica no está bajo demanda en un controlador determinado.
- Otras características se están implementando en primer lugar.

Queremos que todos los controladores admitan todas las características y dedicamos esfuerzos para garantizar la paridad de características entre los controladores. Sin embargo, no siempre es posible conseguirlo. A fin de ayudarle a elegir el controlador adecuado para sus necesidades, aquí se muestra una lista de características populares y los controladores que las implementan.

- [.NET](#table1)
- [ODBC](#table2)
- [OLE DB](#table2)
- [JDBC](#table2)
- [PHP](#table3)
- [Node.js/JavaScript](#table3)
- [Python](#table3)

| <a id="table1"></a>Característica | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Core)](ado-net/microsoft-ado-net-sql-server.md) | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Framework)](ado-net/microsoft-ado-net-sql-server.md) | System.<wbr>Data.<wbr>SqlClient (.NET Core) | [System.<wbr>Data.<wbr>SqlClient (.NET Framework)](/dotnet/framework/data/adonet/sql/) |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [Sí](ado-net/sql/sqlclient-support-always-encrypted.md) | [Sí](ado-net/sql/sqlclient-support-always-encrypted.md) | | [Sí](ado-net/sql/sqlclient-support-always-encrypted.md) |
| [Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [Sí](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | [Sí](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | | [Sí](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) |
| [Autenticación de token de acceso de Azure Active Directory](/azure/active-directory/develop/access-tokens) | [Sí](/dotnet/api/system.data.sqlclient.sqlconnection.accesstoken) | [Sí](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [Sí](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [Sí](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) |
| [Autenticación de contraseña de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | Sí | Sí | | Sí |
| [Autenticación integrada de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | Sí | Sí | | Sí |
| [Autenticación interactiva (MFA) de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | Sí | Sí | | Sí |
| [Autenticación de identidad administrada de Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/overview) | | | | |
| [Autenticación de entidad de servicio de Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals) | Sí | Sí | | |
| [Autenticación integrada de Windows](/windows-server/security/windows-authentication/windows-authentication-overview) | [Sí](ado-net/sql/authentication-sql-server.md) | [Sí](ado-net/sql/authentication-sql-server.md) | [Sí](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) | [Sí](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) |
| [Copia masiva](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [Sí](ado-net/sql/bulk-copy-operations-sql-server.md) | [Sí](ado-net/sql/bulk-copy-operations-sql-server.md) | [Sí](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) | [Sí](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) |
| [Confidencialidad de los datos y metadatos de clasificación](../relational-databases/security/sql-data-discovery-and-classification.md) | Sí | Sí | Sí | Sí |
| [Conjuntos de resultados activos múltiples (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sí](ado-net/sql/multiple-active-result-sets-mars.md) | [Sí](ado-net/sql/multiple-active-result-sets-mars.md) | [Sí](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) | [Sí](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) |
| [Tipo de datos espaciales](../relational-databases/spatial/spatial-data-sql-server.md) | | Sí | | Sí |
| [Parámetros con valores de tabla (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [Sí](ado-net/sql/table-valued-parameters.md) | [Sí](ado-net/sql/table-valued-parameters.md) | [Sí](/dotnet/framework/data/adonet/sql/table-valued-parameters) | [Sí](/dotnet/framework/data/adonet/sql/table-valued-parameters) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netcore-1.0) | [Sí](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netframework-4.8) |
| [Resolución de IP de red transparente](odbc/using-transparent-network-ip-resolution.md) | | [Sí](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-1.1) | | [Sí](/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring?view=netframework-4.8) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table2"></a>Característica | [ODBC Driver for SQL Server en Windows](odbc/microsoft-odbc-driver-for-sql-server.md) | [ODBC Driver for SQL Server en Linux y macOS](odbc/microsoft-odbc-driver-for-sql-server.md) | [Controlador JDBC en SQL Server](jdbc/microsoft-jdbc-driver-for-sql-server.md) | [Controlador OLE DB para SQL Server](oledb/oledb-driver-for-sql-server.md) |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [Sí](odbc/using-always-encrypted-with-the-odbc-driver.md) | [Sí](odbc/using-always-encrypted-with-the-odbc-driver.md) | [Sí](jdbc/using-always-encrypted-with-the-jdbc-driver.md) |
| [Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [Sí](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [Sí](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [Sí](jdbc/using-always-encrypted-with-the-jdbc-driver.md) | |
| [Autenticación de token de acceso de Azure Active Directory](/azure/active-directory/develop/access-tokens) | [Sí](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [Sí](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [Sí](jdbc/connecting-using-azure-active-directory-authentication.md#connecting-using-access-token) | [Sí](oledb/features/using-azure-active-directory.md) |
| [Autenticación de contraseña de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) |  [Sí](odbc/using-azure-active-directory.md) | [Sí](odbc/using-azure-active-directory.md)<sup>[1](#note1)</sup> | [Sí](jdbc/connecting-using-azure-active-directory-authentication.md) | [Sí](oledb/features/using-azure-active-directory.md) |
| [Autenticación integrada de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sí](odbc/using-azure-active-directory.md) | | [Sí](jdbc/connecting-using-azure-active-directory-authentication.md) | [Sí](oledb/features/using-azure-active-directory.md) |
| [Autenticación interactiva (MFA) de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sí](odbc/using-azure-active-directory.md) | | | [Sí](oledb/features/using-azure-active-directory.md) |
| [Autenticación de identidad administrada de Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/overview) | [Sí](odbc/using-azure-active-directory.md) | [Sí](odbc/using-azure-active-directory.md) | [Sí](jdbc/connecting-using-azure-active-directory-authentication.md) | [Sí](oledb/features/using-azure-active-directory.md) |
| [Autenticación de entidad de servicio de Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Autenticación integrada de Windows](/windows-server/security/windows-authentication/windows-authentication-overview) | Sí | [Sí](odbc/linux-mac/using-integrated-authentication.md) | [Sí](jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) | Sí |
| [Copia masiva](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [Sí](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [Sí](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [Sí](jdbc/using-bulk-copy-with-the-jdbc-driver.md) | [Sí](oledb/features/performing-bulk-copy-operations.md) |
| [Detección de datos y metadatos de clasificación](../relational-databases/security/sql-data-discovery-and-classification.md) | [Sí](odbc/data-classification.md) | [Sí](odbc/data-classification.md) | [Sí](jdbc/data-discovery-classification-sample.md) | |
| [Conjuntos de resultados activos múltiples (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sí](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sí](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | | [Sí](oledb/features/using-multiple-active-result-sets-mars.md) |
| [Tipo de datos espaciales](../relational-databases/spatial/spatial-data-sql-server.md) | | | [Sí](jdbc/use-spatial-datatypes.md) | |
| [Parámetros con valores de tabla (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [Sí](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [Sí](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [Sí](jdbc/using-table-valued-parameters.md) | [Sí](oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) | [Sí](oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [Resolución de IP de red transparente](odbc/using-transparent-network-ip-resolution.md) | [Sí](odbc/using-transparent-network-ip-resolution.md) | [Sí](odbc/using-transparent-network-ip-resolution.md) | [Sí](jdbc/setting-the-connection-properties.md) | [Sí](oledb/features/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table3"></a>Característica | [Controladores de PHP para SQL Server en Windows](php/microsoft-php-driver-for-sql-server.md)<sup>[2](#note2)</sup> | [Controladores de PHP para SQL Server en Linux y macOS](php/microsoft-php-driver-for-sql-server.md)<sup>[2](#note2)</sup> | [Tedious (Node.js)](node-js/node-js-driver-for-sql-server.md) | [pyODBC (Python)](python/pyodbc/python-sql-driver-pyodbc.md)<sup>[2](#note2)</sup> |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [Sí](php/using-always-encrypted-php-drivers.md) | [Sí](php/using-always-encrypted-php-drivers.md) | | Sí |
| [Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [Sí](php/always-encrypted-secure-enclaves.md) | [Sí](php/always-encrypted-secure-enclaves.md) | | Sí |
| [Autenticación de token de acceso de Azure Active Directory](/azure/active-directory/develop/access-tokens) | [Sí](php/azure-active-directory.md) | [Sí](php/azure-active-directory.md) | [Sí](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | Sí |
| [Autenticación de contraseña de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sí](php/azure-active-directory.md) | [Sí](php/azure-active-directory.md)<sup>[1](#note1)</sup> | [Sí](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | Sí |
| [Autenticación integrada de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | | | | Sí<sup>[3](#note3)</sup> |
| [Autenticación interactiva (MFA) de Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | | | | Sí<sup>[3](#note3)</sup> |
| [Autenticación de identidad administrada de Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/overview) | [Sí](php/azure-active-directory.md) | [Sí](php/azure-active-directory.md) | [Sí](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | Sí |
| [Autenticación de entidad de servicio de Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Autenticación integrada de Windows](/windows-server/security/windows-authentication/windows-authentication-overview) | [Sí](php/how-to-connect-using-windows-authentication.md) | [Sí](odbc/linux-mac/using-integrated-authentication.md) | | Sí |
| [Copia masiva](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | | | [Sí](https://tediousjs.github.io/tedious/bulk-load.html) | |
| [Detección de datos y metadatos de clasificación](../relational-databases/security/sql-data-discovery-and-classification.md) | Sí | Sí | | |
| [Conjuntos de resultados activos múltiples (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sí](php/how-to-disable-multiple-active-resultsets-mars.md) | [Sí](php/how-to-disable-multiple-active-resultsets-mars.md) | | Sí |
| [Tipo de datos espaciales](../relational-databases/spatial/spatial-data-sql-server.md) | | | | |
| [Parámetros con valores de tabla (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | | | [Sí](https://tediousjs.github.io/tedious/parameters.html) | Sí |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sí](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [Sí](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [Sí](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [Resolución de IP de red transparente](odbc/using-transparent-network-ip-resolution.md) | [Sí](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [Sí](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [Sí](odbc/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<a id="note1"></a><sup>1</sup> La autenticación federada de Active Directory sin sincronización de hash de contraseñas o la autenticación de paso a través no es compatible con Linux y macOS.

<a id="note2"></a><sup>2</sup> Debido a que estos controladores se basan en Microsoft ODBC Driver for SQL Server, también se debe usar una versión de ese controlador que admita la característica.

<a id="note3"></a><sup>3</sup> Solo en Windows.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
