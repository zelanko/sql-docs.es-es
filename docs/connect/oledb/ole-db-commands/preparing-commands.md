---
title: Preparar comandos | Microsoft Docs
description: Preparar comandos mediante el controlador de OLE DB para SQL Server
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
- OLE DB Driver for SQL Server, commands
- prepared statements [OLE DB Driver for SQL Server]
- commands [OLE DB]
- command preparation [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b5cefe4cea0c0d156c13239f24c4a97f7c90eeb0
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106021"
---
# <a name="preparing-commands"></a>Preparar comandos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server admite la preparación de comandos para la ejecución múltiple y optimizada de un único comando; en cambio, la preparación de comandos genera una sobrecarga y no es necesario que un consumidor prepare un comando para ejecutarlo más de una vez. En general, un comando debería prepararse si va a ejecutarse más de tres veces.  
  
 Por razones de rendimiento, la preparación del comando se difiere hasta que se ejecuta el comando. Éste es el comportamiento predeterminado. Cualquier error que se produzca en el comando que se está preparando no se dará a conocer hasta que el comando se ejecute o hasta que se realice una operación de metapropiedad. Establecer la propiedad SSPROP_DEFERPREPARE de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en FALSE puede desactivar este comportamiento predeterminado.  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], cuando un comando se ejecuta directamente (sin prepararlo antes), se crea un plan de ejecución y se almacena en la memoria caché. Si vuelve a ejecutarse la instrucción SQL, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dispone de un algoritmo eficaz para hacer coincidir la nueva instrucción con el plan de ejecución existente en la memoria caché, y reutiliza el plan de ejecución para esa instrucción.  
  
 En el caso de los comandos preparados, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona compatibilidad nativa para preparar y ejecutar instrucciones de comandos. Cuando se prepara una instrucción, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea un plan de ejecución, lo almacena en la memoria caché y devuelve un identificador a este plan de ejecución al proveedor. A continuación, el proveedor utiliza este identificador para ejecutar repetidamente la instrucción. No se crea ningún procedimiento almacenado. Dado que el identificador identifica directamente el plan de ejecución de una instrucción SQL en lugar de hacer coincidir la instrucción con el plan de ejecución de la memoria caché (como ocurre con la ejecución directa), resulta más eficaz preparar una instrucción que ejecutarla directamente, si sabe que la instrucción se ejecutará bastantes veces.  
  
 En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], las instrucciones preparadas no pueden utilizarse para crear objetos temporales ni pueden hacer referencia a procedimientos almacenados del sistema que crean objetos temporales, como tablas temporales. Estos procedimientos deben ejecutarse directamente.  
  
 Algunos comandos no deberían prepararse nunca. Por ejemplo, no deberían prepararse nunca los comandos que especifican la ejecución de procedimientos almacenados o los comandos que incluyen texto que no es válido para la creación de procedimientos almacenados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Si se crea un procedimiento almacenado temporal, el controlador OLE DB para SQL Server lo ejecuta y devuelve los resultados como si se hubiera ejecutado la propia instrucción.  
  
 La propiedad de inicialización SSPROP_INIT_USEPROCFORPREP específica del controlador OLE DB para SQL Server controla la creación del procedimiento almacenado temporal. Si el valor de la propiedad es SSPROPVAL_USEPROCFORPREP_ON o SSPROPVAL_USEPROCFORPREP_ON_DROP, el controlador OLE DB para SQL Server intenta crear un procedimiento almacenado cuando se prepara un comando. La creación del procedimiento almacenado se realiza correctamente si el usuario de la aplicación tiene suficientes permisos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 En el caso de los consumidores que se desconectan con poca frecuencia, la creación de procedimientos almacenados temporales puede requerir recursos significativos de **tempdb**, la base de datos del sistema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que se crean los objetos temporales. Si el valor de SSPROP_INIT_USEPROCFORPREP es SSPROPVAL_USEPROCFORPREP_ON, los procedimientos almacenados temporales creados por el controlador OLE DB para SQL Server solo se quitan cuando la sesión que ha creado el comando pierde su conexión con la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si esa conexión es la conexión predeterminada creada durante la inicialización del origen de datos, el procedimiento almacenado temporal solamente se quita cuando se cancela la inicialización del origen de datos.  
  
 Si el valor de SSPROP_INIT_USEPROCFORPREP es SSPROPVAL_USEPROCFORPREP_ON_DROP, los procedimientos almacenados temporales del controlador OLE DB para SQL Server se quitan cuando se produce una de estas situaciones:  
  
-   El consumidor usa **ICommandText::SetCommandText** para indicar un nuevo comando.  
  
-   El consumidor usa **ICommandPrepare::Unprepare** para indicar que ya no requiere el texto del comando.  
  
-   El consumidor libera todas las referencias al objeto de comando utilizando el procedimiento almacenado temporal.  
  
 Un objeto de comando tiene a lo sumo un procedimiento almacenado temporal en **tempdb**. Cualquier procedimiento almacenado temporal existente representa el texto de comando actual de un objeto de comando concreto.  
  
## <a name="see-also"></a>Ver también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
