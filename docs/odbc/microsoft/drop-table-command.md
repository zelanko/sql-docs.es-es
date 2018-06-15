---
title: Comando DROP TABLE | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 657f175f52f7a098a2c026cf384fdf1b77f43484
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900200"
---
# <a name="drop-table-command"></a>Comando DROP TABLE
Quita una tabla de la base de datos especificada con el origen de datos y lo elimina del disco.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativo para este comando. Para obtener información específica del controlador, vea la sección Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Configuración  
 *TableName*  
 Especifica la tabla que se va a quitar de la base de datos especificada con el origen de datos como eliminar del disco.  
  
 *FileName*  
 Especifica una tabla libre para eliminar desde el disco.  
  
 ?  
 Muestra el cuadro de diálogo Quitar desde el que puede elegir una tabla que se va a quitar de la base de datos especificada con el origen de datos como eliminar del disco.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se emite DROP TABLE, también se quitan todos los índices principales, valores predeterminados y reglas de validación asociadas a la tabla. DROP TABLE también afecta a otras tablas de la base de datos especificada con el origen de datos si las tablas tienen reglas o las relaciones asociadas con la tabla que se va a quitar. Las relaciones y reglas ya no son válidas cuando se quita la tabla de la base de datos.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción DROP TABLE de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando de tabla de FoxProDROP Visual mediante la sintaxis mostrada en la tabla siguiente.  
  
|Sintaxis de ODBC|Origen de datos|Sintaxis de Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *nombre de la tabla de base*|Base de datos (archivo .dbc)|Quitar tabla *TableName* eliminar|  
||Directorio de tablas libres (archivos)|Borrar *dbfName*<br /><br /> Borrar *cdxName*<br /><br /> Borrar *fptName*|
