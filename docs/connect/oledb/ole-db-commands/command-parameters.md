---
title: Parámetros de comando | Documentos de Microsoft
description: Parámetros de comando
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9358369e5c6c5c57bc6000689f831a405d16e5d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="command-parameters"></a>Parámetros de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los parámetros se marcan en el texto de comando con el carácter de signo de interrogación de cierre. Por ejemplo, la siguiente instrucción SQL está marcada para un único parámetro de entrada:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Para mejorar el rendimiento al reducir el tráfico de red, el controlador OLE DB para SQL Server no deriva automáticamente la información de parámetros a menos que **ICommandWithParameters:: GetParameterInfo** o **ICommandPrepare:: Preparar** se llama antes de ejecutar un comando. Esto significa que el controlador OLE DB para SQL Server no automáticamente:  
  
-   Comprobar la exactitud del tipo de datos especificado con **ICommandWithParameters:: SetParameterInfo**.  
  
-   Asignar el DBTYPE especificado en la información de enlace del descriptor de acceso al tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] correcto para el parámetro.  
  
 Las aplicaciones recibirán posibles errores o pérdidas de precisión con cualquiera de estos métodos si especifican tipos de datos que no son compatibles con el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del parámetro.  
  
 Para asegurarse de que esto no ocurra, la aplicación debe:  
  
-   Asegúrese de que *pwszDataSourceType* coincide con la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de tipo de datos para el parámetro si codificar de forma rígida **ICommandWithParameters:: SetParameterInfo**.  
  
-   Asegurarse de que el valor DBTYPE enlazado al parámetro sea del mismo tipo que el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el parámetro si se incluye un descriptor de acceso en el código.  
  
-   Codificar la aplicación para llamar a **ICommandWithParameters:: GetParameterInfo** para que el proveedor pueda obtener el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos de los parámetros dinámicamente. Tenga en cuenta que esto provoca un viaje de ida y vuelta (round trip) adicional de la red al servidor.  
  
> [!NOTE]  
>  El proveedor no permite llamar a **ICommandWithParameters:: GetParameterInfo** para cualquier [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instrucción UPDATE o DELETE que contenga una cláusula FROM; para cualquier instrucción SQL que dependa una subconsulta que contiene parámetros; para las instrucciones SQL que contiene marcadores de parámetros en las dos expresiones de una comparación like o cuantificado predicado; o consultas donde uno de los parámetros es un parámetro a una función. Al procesar un lote de instrucciones SQL, el proveedor también no permite llamar a **ICommandWithParameters:: GetParameterInfo** marcadores de parámetros en instrucciones después de la primera instrucción del lote. Comentarios (/ * \*/) no están permitidas en el [!INCLUDE[tsql](../../../includes/tsql-md.md)] comando.  
  
 El controlador OLE DB para SQL Server admite parámetros de entrada en los comandos de instrucción SQL. En los comandos de la llamada a procedimiento, el controlador OLE DB para SQL Server admite parámetros de entrada, salida y entrada/salida. Los valores de los parámetros de salida se devuelven a la aplicación en ejecución (únicamente si no se ha devuelto ningún conjunto de filas) o cuando la aplicación agota todos los conjuntos de filas. Para asegurarse de que los valores devueltos son válidos, utilice **IMultipleResults** para forzar el consumo de conjunto de filas.  
  
 No es necesario especificar los nombres de los parámetros de procedimientos almacenados en una estructura DBPARAMBINDINFO. Utilice NULL para el valor de la *pwszName* miembro para indicar que el controlador OLE DB para SQL Server debe omitir el nombre del parámetro y utilizar únicamente el ordinal especificado en el *rgParamOrdinals* miembro de  **ICommandWithParameters:: SetParameterInfo**. Si el texto del comando contiene tanto parámetros con nombre como parámetros sin nombre, todos los parámetros sin nombre deben especificarse antes de cualquier parámetro con nombre.  
  
 Si se especifica el nombre de un parámetro de procedimiento almacenado, el controlador OLE DB para SQL Server comprueba el nombre para asegurarse de que es válido. El controlador OLE DB para SQL Server devuelve un error cuando recibe un nombre de parámetro erróneo del consumidor.  
  
> [!NOTE]  
>  Para exponer la compatibilidad para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML y tipos definidos por el usuario (UDT), el controlador OLE DB para SQL Server implementa una nueva [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) interfaz.  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
