---
title: Parámetros de comando | Microsoft Docs
description: Parámetros de comando
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 26aac2c295d209c30efb7098b92e8a746390a886
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033795"
---
# <a name="command-parameters"></a>Parámetros de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los parámetros se marcan en el texto de comando con el carácter de signo de interrogación de cierre. Por ejemplo, la siguiente instrucción SQL está marcada para un único parámetro de entrada:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Para mejorar el rendimiento mediante la reducción del tráfico de red, el controlador OLE DB para SQL Server no deriva automáticamente la información de parámetros a menos que se llame a **ICommandWithParameters::GetParameterInfo** o **ICommandPrepare::Prepare** antes de ejecutar un comando. Esto significa que el controlador OLE DB para SQL Server no automáticamente:  
  
-   Comprobar la exactitud del tipo de datos especificado con **ICommandWithParameters::SetParameterInfo**.  
  
-   Asignar el DBTYPE especificado en la información de enlace del descriptor de acceso al tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] correcto para el parámetro.  
  
 Las aplicaciones recibirán posibles errores o pérdidas de precisión con cualquiera de estos métodos si especifican tipos de datos que no son compatibles con el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del parámetro.  
  
 Para asegurarse de que esto no ocurra, la aplicación debe:  
  
-   Asegurarse de que *pwszDataSourceType* coincida con el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del parámetro si **ICommandWithParameters::SetParameterInfo** está codificado de forma rígida.  
  
-   Asegurarse de que el valor DBTYPE enlazado al parámetro sea del mismo tipo que el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el parámetro si se incluye un descriptor de acceso en el código.  
  
-   Programar la aplicación para llamar a **ICommandWithParameters::GetParameterInfo** de forma que el proveedor pueda obtener dinámicamente los tipos de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de los parámetros. Tenga en cuenta que esto provoca un viaje de ida y vuelta (round trip) adicional de la red al servidor.  
  
> [!NOTE]  
>  El proveedor no permite que se llame a **ICommandWithParameters::GetParameterInfo** para ninguna instrucción UPDATE o DELETE de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contenga una cláusula FROM; para ninguna instrucción SQL que dependa de una subconsulta que contenga parámetros; para instrucciones SQL que contengan marcadores de parámetros en las dos expresiones de una comparación, igualdad o predicado cuantificado; o consultas donde uno de los parámetros sea un parámetro de una función. Al procesar un lote de instrucciones SQL, el proveedor tampoco admite que se llame a **ICommandWithParameters::GetParameterInfo** para marcadores de parámetros en instrucciones después de la primera instrucción del lote. No se permiten comentarios (/* \*/) en el comando [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 El controlador OLE DB para SQL Server admite los parámetros de entrada en los comandos de instrucción SQL. En los comandos de la llamada de procedimiento, el controlador OLE DB para SQL Server es compatible con parámetros de entrada, salida y entrada/salida. Los valores de los parámetros de salida se devuelven a la aplicación en ejecución (únicamente si no se ha devuelto ningún conjunto de filas) o cuando la aplicación agota todos los conjuntos de filas. Para asegurarse de que los valores devueltos sean válidos, use **IMultipleResults** para forzar el consumo del conjunto de filas.  
  
 No es necesario especificar los nombres de los parámetros de procedimientos almacenados en una estructura DBPARAMBINDINFO. Use NULL para el valor del miembro *pwszName* a fin de indicar que el controlador OLE DB para SQL Server debe omitir el nombre del parámetro y usar solo el ordinal especificado en el miembro *rgParamOrdinals* de **ICommandWithParameters::SetParameterInfo**. Si el texto del comando contiene tanto parámetros con nombre como parámetros sin nombre, todos los parámetros sin nombre deben especificarse antes de cualquier parámetro con nombre.  
  
 Si se especifica el nombre de un parámetro de procedimiento almacenado, el controlador OLE DB para SQL Server lo comprueba para asegurarse de que es válido. El controlador OLE DB para SQL Server devuelve un error cuando recibe un nombre de parámetro erróneo del consumidor.  
  
> [!NOTE]  
>  Para exponer la compatibilidad con XML y tipos definidos por el usuario (UDT) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador OLE DB para SQL Server implementa una nueva interfaz [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
## <a name="see-also"></a>Ver también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
