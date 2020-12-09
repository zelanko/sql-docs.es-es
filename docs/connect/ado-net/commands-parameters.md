---
title: Comandos y parámetros
description: Obtenga información sobre cómo usar objetos de comando para el proveedor de datos SqlClient de Microsoft para SQL Server para ejecutar comandos y devolver resultados de un origen de datos.
ms.date: 11/25/2020
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 931c36619f5eaed0159ee04db3a08eb745634698
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428318"
---
# <a name="commands-and-parameters"></a>Comandos y parámetros

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Una vez establecida una conexión a un origen de datos, puede ejecutar comandos y devolver resultados desde el mismo mediante un objeto <xref:System.Data.Common.DbCommand>. Puede crear un comando mediante uno de los constructores de comandos para el proveedor de datos SqlClient de Microsoft para SQL Server. Los constructores pueden aceptar argumentos opcionales, como una instrucción SQL para ejecutar en el origen de datos, un objeto <xref:System.Data.Common.DbConnection> o un objeto <xref:System.Data.Common.DbTransaction>.

También puede configurar dichos objetos como propiedades del comando. También puede crear un comando para una determinada conexión mediante el método <xref:System.Data.Common.DbConnection.CreateCommand%2A> de un objeto `DbConnection`. La instrucción SQL que ejecuta el comando se puede configurar mediante la propiedad <xref:System.Data.Common.DbCommand.CommandText%2A>. El proveedor de datos SqlClient de Microsoft para SQL Server tiene el objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

## <a name="in-this-section"></a>En esta sección

[Ejecución de un comando](execute-command.md) Describe el objeto `Command` de ADO.NET y cómo usarlo para ejecutar consultas y comandos en un origen de datos.

[Configuración de parámetros](configure-parameters.md) Describe el trabajo con parámetros `Command`, como la dirección, los tipos de datos y la sintaxis de los parámetros.

[Generación de comandos con objetos CommandBuilder](generate-commands-with-commandbuilders.md)  
Describe cómo utilizar generadores de comandos para generar automáticamente comandos INSERT, UPDATE y DELETE para un `DataAdapter` que tiene un comando SELECT de tabla única.

[Obtención de un valor único de una base de datos](obtain-single-value-from-database.md) Describe cómo utilizar el método `ExecuteScalar` de un objeto `Command` para devolver un valor único de una consulta de base de datos.

[Uso de comandos para modificar datos](use-commands-to-modify-data.md) Describe cómo usar el proveedor de datos SqlClient de Microsoft para SQL Server para ejecutar procedimientos almacenados o instrucciones de lenguaje de definición de datos (DDL).

## <a name="see-also"></a>Vea también

- [Conexión a un origen de datos](connecting-to-data-source.md)
