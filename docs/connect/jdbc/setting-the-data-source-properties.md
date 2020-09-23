---
title: Establecimiento de las propiedades de origen de datos
description: Obtenga información sobre los orígenes de datos en JDBC y cómo establecer sus propiedades para configurar el acceso a bases de datos con Java.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a2a9964b592fc1bcb8c41cf0c5b8de67a2d5a18
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411341"
---
# <a name="setting-the-data-source-properties"></a>Establecimiento de las propiedades de origen de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Los orígenes de datos son el mecanismo preferido por el que crear conexiones de JDBC en un entorno Java Platform, Enterprise Edition (Java EE). Los orígenes de datos proporcionan conexiones, conexiones agrupadas y conexiones distribuidas sin codificar de forma rígida las propiedades de la conexión en código Java. Todos los orígenes de datos del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pueden establecer u obtener el valor de cualquier propiedad mediante los métodos adecuados de establecedor y captador, respectivamente.

Los productos de Java EE, tales como servidores de aplicaciones y motores de servlet/JSP, normalmente le permiten configurar los orígenes de datos para el acceso a bases de datos. Todas las propiedades enumeradas en el tema [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) se pueden especificar siempre que la configuración permita escribir una propiedad como un par propiedad=valor.

Para obtener más información sobre los orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea la clase [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). Para obtener un ejemplo de cómo usar la clase SQLServerDataSource para establecer una conexión con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Ejemplo de origen de datos](../../connect/jdbc/data-source-sample.md).

## <a name="see-also"></a>Consulte también

[Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
