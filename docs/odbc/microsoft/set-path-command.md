---
title: Comando de ruta de acceso SET | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3d810e66249779b2d3706e92ea39f89a0f87cff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159250"
---
# <a name="set-path-command"></a>Comando de ruta de acceso set
Especifica una ruta de acceso para búsquedas de archivos. Para obtener información específica del controlador, vea la sección Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumentos  
 A [ *ruta*]  
 Especifica los directorios de Visual FoxPro a buscar. Use comas o punto y coma para separar los directorios.  
  
## <a name="remarks"></a>Comentarios  
 Establecer ruta de acceso le permite especificar las rutas de búsqueda para otros programas de Visual FoxPro que se pueden llamar dentro de procedimientos almacenados. Establecer ruta de acceso no cambiará la ruta de acceso del origen de datos que ha especificado para la conexión.  
  
 Emitir establecer ruta de acceso a sin *ruta* para restaurar la ruta de acceso al directorio predeterminado o la carpeta.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Si emite establecer ruta de acceso en un procedimiento almacenado, se omitirán mediante los comandos y las funciones siguientes:  
  
-   Funciones de catálogo como [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) y [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) omitirá la nueva ruta de acceso y continuar hacer referencia a la ruta de acceso especificada por el origen de datos en [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) o [ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Omitirá la nueva ruta de acceso y continuar hacer referencia a la ruta de acceso especificada por el origen de datos en comandos como SELECT, INSERT, UPDATE, DELETE y CREATE TABLE **SQLPrepare** o **SQLExecDirect**.  
  
 Si emitir establecer ruta de acceso en un procedimiento almacenado y posteriormente no establece la ruta de acceso a su estado original, las otras conexiones con la base de datos usará la nueva ruta de acceso (ya que establece la ruta de acceso no está dirigida a las sesiones de datos).  
  
 Si desea crear, seleccionar o actualizar las tablas en un directorio distinto del especificado por el origen de datos, especifique la ruta de acceso completa del archivo con el comando.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de instalación de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
