---
title: Parámetros de comando | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 805af790d5a703f1fefca6173b119586b002bd95
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39550775"
---
# <a name="command-parameters"></a>Parámetros de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los parámetros se marcan en el texto de comando con el carácter de signo de interrogación de cierre. Por ejemplo, la siguiente instrucción SQL está marcada para un único parámetro de entrada:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Para mejorar el rendimiento al reducir el tráfico de red, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no deriva automáticamente la información de parámetros, a menos que **ICommandWithParameters:: GetParameterInfo** o  **ICommandPrepare:: Prepare** se llama antes de ejecutar un comando. Esto significa que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no automáticamente:  
  
-   Comprobar la exactitud del tipo de datos especificado con **ICommandWithParameters::SetParameterInfo**.  
  
-   Asignar el DBTYPE especificado en la información de enlace del descriptor de acceso al tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correcto para el parámetro.  
  
 Las aplicaciones recibirán posibles errores o pérdidas de precisión con cualquiera de estos métodos si especifican tipos de datos que no son compatibles con el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del parámetro.  
  
 Para asegurarse de que esto no ocurra, la aplicación debe:  
  
-   Asegurarse de que *pwszDataSourceType* coincida con el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del parámetro si **ICommandWithParameters::SetParameterInfo** está codificado de forma rígida.  
  
-   Asegurarse de que el valor DBTYPE enlazado al parámetro sea del mismo tipo que el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el parámetro si se incluye un descriptor de acceso en el código.  
  
-   Programar la aplicación para llamar a **ICommandWithParameters::GetParameterInfo** de forma que el proveedor pueda obtener dinámicamente los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de los parámetros. Tenga en cuenta que esto provoca un viaje de ida y vuelta (round trip) adicional de la red al servidor.  
  
> [!NOTE]  
>  El proveedor no permite que se llame a **ICommandWithParameters::GetParameterInfo** para ninguna instrucción UPDATE o DELETE de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contenga una cláusula FROM; para ninguna instrucción SQL que dependa de una subconsulta que contenga parámetros; para instrucciones SQL que contengan marcadores de parámetros en las dos expresiones de una comparación, igualdad o predicado cuantificado; o consultas donde uno de los parámetros sea un parámetro de una función. Al procesar un lote de instrucciones SQL, el proveedor tampoco admite que se llame a **ICommandWithParameters::GetParameterInfo** para marcadores de parámetros en instrucciones después de la primera instrucción del lote. No se permiten comentarios (/* \*/) en el comando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite parámetros de entrada en los comandos de instrucción SQL. En los comandos de la llamada de procedimiento, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite parámetros de entrada, salida y entrada/salida. Los valores de los parámetros de salida se devuelven a la aplicación en ejecución (únicamente si no se ha devuelto ningún conjunto de filas) o cuando la aplicación agota todos los conjuntos de filas. Para asegurarse de que los valores devueltos sean válidos, use **IMultipleResults** para forzar el consumo del conjunto de filas.  
  
 No es necesario especificar los nombres de los parámetros de procedimientos almacenados en una estructura DBPARAMBINDINFO. Utilice NULL para el valor de la *pwszName* miembro para indicar que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client debe omitir el nombre del parámetro y utilizar únicamente el ordinal especificado en el *rgParamOrdinals*miembro **ICommandWithParameters:: SetParameterInfo**. Si el texto del comando contiene tanto parámetros con nombre como parámetros sin nombre, todos los parámetros sin nombre deben especificarse antes de cualquier parámetro con nombre.  
  
 Si se especifica el nombre de un parámetro de procedimiento almacenado, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client comprueba el nombre para asegurarse de que es válido. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve un error cuando recibe un nombre de parámetro erróneo del consumidor.  
  
> [!NOTE]  
>  Para exponer la compatibilidad para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML y tipos definidos por el usuario (UDT), el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client implementa una nueva [ISSCommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) interfaz.  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
