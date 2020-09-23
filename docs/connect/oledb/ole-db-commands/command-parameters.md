---
title: Parámetros de comando (controlador OLE DB) | Microsoft Docs
description: Obtenga información sobre los parámetros de comando, incluidos los tipos que admite OLE DB Driver for SQL Server para la instrucción SQL y los comandos de llamadas a procedimientos.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c7266c3fd59e9883cb59ae81f42f651c2ea2b3e
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860175"
---
# <a name="command-parameters"></a>Parámetros de comando
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los parámetros se marcan en el texto de comando con el carácter de signo de interrogación de cierre. Por ejemplo, la siguiente instrucción SQL está marcada para un único parámetro de entrada:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Para mejorar el rendimiento mediante la reducción del tráfico de red, el controlador OLE DB para SQL Server no deriva automáticamente la información de parámetros a menos que se llame a **ICommandWithParameters::GetParameterInfo** o **ICommandPrepare::Prepare** antes de ejecutar un comando. Esto significa que OLE DB Driver for SQL Server no hace automáticamente nada de lo siguiente:  
  
-   Comprobar la exactitud del tipo de datos especificado con **ICommandWithParameters::SetParameterInfo**.  
  
-   Asignar el DBTYPE especificado en la información de enlace del descriptor de acceso al tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] correcto para el parámetro.  
  
 Las aplicaciones recibirán posibles errores o pérdidas de precisión con cualquiera de estos métodos si especifican tipos de datos que no son compatibles con el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del parámetro.  
  
 Para asegurarse de que esto no ocurra, la aplicación debe:  
  
-   Asegurarse de que *pwszDataSourceType* coincida con el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del parámetro si **ICommandWithParameters::SetParameterInfo** está codificado de forma rígida.  
  
-   Asegurarse de que el valor DBTYPE enlazado al parámetro sea del mismo tipo que el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el parámetro si se incluye un descriptor de acceso en el código.  
  
-   Programar la aplicación para llamar a **ICommandWithParameters::GetParameterInfo** de forma que el proveedor pueda obtener dinámicamente los tipos de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de los parámetros. Tenga en cuenta que esto provoca un viaje de ida y vuelta (round trip) adicional de la red al servidor.  
  
> [!NOTE]  
>  El proveedor no permite que se llame a **ICommandWithParameters::GetParameterInfo** para ninguna instrucción UPDATE o DELETE de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contenga una cláusula FROM; para ninguna instrucción SQL que dependa de una subconsulta que contenga parámetros; para instrucciones SQL que contengan marcadores de parámetros en las dos expresiones de una comparación, igualdad o predicado cuantificado; o consultas donde uno de los parámetros sea un parámetro de una función. Al procesar un lote de instrucciones SQL, el proveedor tampoco admite que se llame a **ICommandWithParameters::GetParameterInfo** para marcadores de parámetros en instrucciones después de la primera instrucción del lote. No se permiten comentarios (/* \*/) en el comando [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 OLE DB Driver for SQL Server admite parámetros de entrada en comandos de instrucciones SQL. En comandos de llamadas a procedimientos, OLE DB Driver for SQL Server admite parámetros de entrada, parámetros de salida y parámetros de entrada y salida. Los valores de los parámetros de salida se devuelven a la aplicación en ejecución (únicamente si no se ha devuelto ningún conjunto de filas) o cuando la aplicación agota todos los conjuntos de filas. Para asegurarse de que los valores devueltos sean válidos, use **IMultipleResults** para forzar el consumo del conjunto de filas.  
  
 No es necesario especificar los nombres de los parámetros de procedimientos almacenados en una estructura DBPARAMBINDINFO. Use NULL para el valor del miembro *pwszName* a fin de indicar que el controlador OLE DB para SQL Server debe omitir el nombre del parámetro y usar solo el ordinal especificado en el miembro *rgParamOrdinals* de **ICommandWithParameters::SetParameterInfo**. Si el texto del comando contiene tanto parámetros con nombre como parámetros sin nombre, todos los parámetros sin nombre deben especificarse antes de cualquier parámetro con nombre.  
  
 Si se especifica el nombre de un parámetro de procedimiento almacenado, el controlador OLE DB para SQL Server lo comprueba para asegurarse de que es válido. OLE DB Driver for SQL Server devuelve un error cuando recibe un nombre de parámetro erróneo por parte del consumidor.  
  
> [!NOTE]  
>  Para exponer la compatibilidad con XML y tipos definidos por el usuario (UDT) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador OLE DB para SQL Server implementa una nueva interfaz [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
## <a name="see-also"></a>Consulte también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
