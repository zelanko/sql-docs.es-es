---
title: Comando SET PATH (SET PATH Command) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e44093c3ea18bc995264a8974726f5af0abe3b3a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300825"
---
# <a name="set-path-command"></a>Comando de ruta de acceso set
Especifica una ruta de acceso para las búsquedas de archivos. Para obtener información específica del controlador, consulte Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumentos  
 A [ *Camino*]  
 Especifica los directorios que desea que Visual FoxPro busque. Utilice comas o punto y coma para separar los directorios.  
  
## <a name="remarks"></a>Observaciones  
 SET PATH le permite especificar rutas de búsqueda para otros programas de Visual FoxPro a los que se puede llamar dentro de procedimientos almacenados. SET PATH no cambiará la ruta de acceso del origen de datos que ha especificado para la conexión.  
  
 Emita SET PATH TO sin *Path* para restaurar la ruta de acceso al directorio o carpeta predeterminado.  
  
## <a name="driver-remarks"></a>Observaciones del conductor  
 Si emite SET PATH en un procedimiento almacenado, las siguientes funciones y comandos lo ignorarán:  
  
-   Las funciones de catálogo como [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) y [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) omitirán la nueva ruta de acceso y seguirán haciendo referencia a la ruta de acceso especificada por el origen de datos en [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) o [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Los comandos como SELECT, INSERT, UPDATE, DELETE y CREATE TABLE omitirán la nueva ruta de acceso y seguirán haciendo referencia a la ruta de acceso especificada por el origen de datos en **SQLPrepare** o **SQLExecDirect**.  
  
 Si emite SET PATH en un procedimiento almacenado y no vuelve a establecer la ruta de acceso a su estado original, otras conexiones a la base de datos usarán la nueva ruta de acceso (porque SET PATH no tiene el ámbito de las sesiones de datos).  
  
 Si desea crear, seleccionar o actualizar tablas en un directorio distinto del especificado por el origen de datos, especifique la ruta de acceso completa del archivo con el comando.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo Configuración de ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (controlador ODBC de Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
