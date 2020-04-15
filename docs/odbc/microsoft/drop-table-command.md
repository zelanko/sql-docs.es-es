---
title: Comando DROP TABLE ??????????? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303426"
---
# <a name="drop-table-command"></a>Comando DROP TABLE
Quita una tabla de la base de datos especificada con el origen de datos y la elimina del disco.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis de lenguaje nativo de Visual FoxPro para este comando. Para obtener información específica del controlador, consulte Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Configuración  
 *TableName*  
 Especifica la tabla que se va a quitar de la base de datos especificada con el origen de datos y se va a eliminar del disco.  
  
 *FileName*  
 Especifica una tabla libre para eliminar del disco.  
  
 ?  
 Muestra el cuadro de diálogo Quitar del que puede elegir una tabla para quitar de la base de datos especificada con el origen de datos y eliminar del disco.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se emite DROP TABLE, también se quitan todos los índices principales, los valores predeterminados y las reglas de validación asociadas a la tabla. DROP TABLE también afecta a otras tablas de la base de datos especificada con el origen de datos si esas tablas tienen reglas o relaciones asociadas con la tabla que se va a quitar. Las reglas y las relaciones ya no son válidas cuando la tabla se quita de la base de datos.  
  
## <a name="driver-remarks"></a>Observaciones del conductor  
 Cuando la aplicación envía la instrucción SQL ODBC DROP TABLE al origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando Visual FoxProDROP TABLE mediante la sintaxis que se muestra en la tabla siguiente.  
  
|Sintaxis ODBC|Origen de datos|Sintaxis de Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *base-table-name*|Base de datos (archivo .dbc)|REMOVE TABLE *TableName* DELETE|  
||Directorio de tablas libres (archivos .dbf)|ERASE *dbfName*<br /><br /> *CDxName* de ERASE<br /><br /> ERASE *fptName*|
