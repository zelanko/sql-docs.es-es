---
title: Preparar comandos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- prepared statements [SQL Server Native Client]
- commands [OLE DB]
- command preparation [SQL Server Native Client]
ms.assetid: 09ec0c6c-0a44-4766-b9b7-5092f676ee54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9dada733f7729d534b66777f747560cd45530727
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865027"
---
# <a name="preparing-commands"></a>Preparar comandos
  El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la preparación de comandos para la ejecución múltiple y optimizada de un único comando; sin embargo, la preparación de comandos genera una sobrecarga, y no es necesario que un consumidor prepare un comando para ejecutarlo más de una vez. En general, un comando debería prepararse si va a ejecutarse más de tres veces.  
  
 Por razones de rendimiento, la preparación del comando se difiere hasta que se ejecuta el comando. Éste es el comportamiento predeterminado. Cualquier error que se produzca en el comando que se está preparando no se dará a conocer hasta que el comando se ejecute o hasta que se realice una operación de metapropiedad. Establecer la propiedad SSPROP_DEFERPREPARE de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en FALSE puede desactivar este comportamiento predeterminado.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cuando un comando se ejecuta directamente (sin prepararlo antes), se crea un plan de ejecución y se almacena en la memoria caché. Si vuelve a ejecutarse la instrucción SQL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone de un algoritmo eficaz para hacer coincidir la nueva instrucción con el plan de ejecución existente en la memoria caché, y reutiliza el plan de ejecución para esa instrucción.  
  
 En el caso de los comandos preparados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona compatibilidad nativa para preparar y ejecutar instrucciones de comandos. Cuando se prepara una instrucción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un plan de ejecución, lo almacena en la memoria caché y devuelve un identificador a este plan de ejecución al proveedor. A continuación, el proveedor utiliza este identificador para ejecutar repetidamente la instrucción. No se crea ningún procedimiento almacenado. Dado que el identificador identifica directamente el plan de ejecución de una instrucción SQL en lugar de hacer coincidir la instrucción con el plan de ejecución de la memoria caché (como ocurre con la ejecución directa), resulta más eficaz preparar una instrucción que ejecutarla directamente, si sabe que la instrucción se ejecutará bastantes veces.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], las instrucciones preparadas no pueden utilizarse para crear objetos temporales ni pueden hacer referencia a procedimientos almacenados del sistema que crean objetos temporales, como tablas temporales. Estos procedimientos deben ejecutarse directamente.  
  
 Algunos comandos no deberían prepararse nunca. Por ejemplo, no deberían prepararse nunca los comandos que especifican la ejecución de procedimientos almacenados o los comandos que incluyen texto que no es válido para la creación de procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si se crea un procedimiento almacenado temporal, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client lo ejecuta y devuelve los resultados como si se hubiera ejecutado la propia instrucción.  
  
 La propiedad de inicialización SSPROP_INIT_USEPROCFORPREP específica del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controla la creación del procedimiento almacenado temporal. Si el valor de la propiedad es SSPROPVAL_USEPROCFORPREP_ON o SSPROPVAL_USEPROCFORPREP_ON_DROP, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client intenta crear un procedimiento almacenado cuando se prepara un comando. La creación del procedimiento almacenado se realiza correctamente si el usuario de la aplicación tiene suficientes permisos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En el caso de los consumidores que se desconectan con poca frecuencia, la creación de procedimientos almacenados temporales puede requerir recursos significativos de **tempdb**, la base de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se crean los objetos temporales. Si el valor de SSPROP_INIT_USEPROCFORPREP es SSPROPVAL_USEPROCFORPREP_ ON, los procedimientos almacenados temporales creados por el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solamente se quitan cuando la sesión que creó el comando pierde su conexión con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si esa conexión es la conexión predeterminada creada durante la inicialización del origen de datos, el procedimiento almacenado temporal solamente se quita cuando se cancela la inicialización del origen de datos.  
  
 Si el valor de SSPROP_INIT_USEPROCFORPREP es SSPROPVAL_USEPROCFORPREP_ON_DROP, los procedimientos almacenados temporales del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se quitan cuando ocurre una de estas cosas:  
  
-   El consumidor usa **ICommandText::SetCommandText** para indicar un nuevo comando.  
  
-   El consumidor usa **ICommandPrepare::Unprepare** para indicar que ya no requiere el texto del comando.  
  
-   El consumidor libera todas las referencias al objeto de comando utilizando el procedimiento almacenado temporal.  
  
 Un objeto de comando tiene a lo sumo un procedimiento almacenado temporal en **tempdb**. Cualquier procedimiento almacenado temporal existente representa el texto de comando actual de un objeto de comando concreto.  
  
## <a name="see-also"></a>Vea también  
 [Comandos](commands.md)  
  
  
