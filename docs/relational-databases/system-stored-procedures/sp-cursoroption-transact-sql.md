---
description: sp_cursoroption (Transact-SQL)
title: sp_cursoroption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1deb0895de1b0a3694465ccb0f9e95228fbedd0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489495"
---
# <a name="sp_cursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Establece las opciones de cursor o devuelve información del cursor creada por el sp_cursoropen procedimiento almacenado. sp_cursoroption se invoca especificando el identificador 8 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Es un valor de *identificador* generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y devuelto por el Sp_cursoropen procedimiento almacenado. el *cursor* requiere un valor de entrada **int** para la ejecución.  
  
 *code*  
 Se usa para estipular varios factores de los valores devueltos del cursor. el *código* requiere uno de los siguientes valores de entrada **int** :  
  
|Value|Nombre|Descripción|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|Devuelve el puntero de texto y no los datos reales, para ciertas columnas de imagen o texto designado.<br /><br /> TEXTPTR_ONLY permite usar punteros de texto como *identificadores* para objetos BLOB que se pueden recuperar o actualizar de forma selectiva mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] o con instalaciones de DBLIB (por ejemplo, [!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT o DBLIB DBWRITETEXT).<br /><br /> Si se asigna el valor "0", todas las columnas de imagen y texto de la lista de selección devolverán punteros de texto en lugar de datos.|  
|0x0002|CURSOR_NAME|Asigna el nombre especificado en el *valor* al cursor. Esto, a su vez, permite a ODBC utilizar [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones UPDATE/DELETE posicionadas en cursores abiertos a través de Sp_cursoropen.<br /><br /> La cadena se puede especificar como cualquier tipo de datos Unicode o de caracteres.<br /><br /> Dado que [!INCLUDE[tsql](../../includes/tsql-md.md)] las instrucciones UPDATE/DELETE colocadas operan, de forma predeterminada, en la primera fila de un cursor FAT, se debe usar SP_CURSOR SETPOSITION para colocar el cursor antes de emitir la instrucción UPDATE/DELETE posicionada.|  
|0x0003|TEXTDATA|Devuelve los datos reales, no el puntero de texto, para ciertas columnas de imagen o texto en las capturas siguientes (es decir, se deshace el efecto de TEXTPTR_ONLY).<br /><br /> Si TEXTDATA está habilitado para una columna en particular, la fila se vuelve a capturar o actualizar, y puede establecerse a continuación de nuevo en TEXTPTR_ONLY. Como con TEXTPTR_ONLY, el parámetro de valor es un entero que especifica el número de columnas y un valor cero devuelve todas las columnas de texto o imagen.|  
|0x0004|SCROLLOPT|Opción de desplazamiento. Vea "Valores del código de retorno", posteriormente en este tema, para obtener información adicional.|  
|0x0005|CCOPT|Opción de control de simultaneidad. Vea "Valores del código de retorno", posteriormente en este tema, para obtener información adicional.|  
|0x0006|ROWCOUNT|El número de filas que están actualmente en el conjunto de resultados.<br /><br /> Nota: el recuento de filas puede haber cambiado desde el valor devuelto por sp_cursoropen si se utiliza el rellenado asincrónico. Se devuelve el valor-1 si se desconoce el número de filas.|  
  
 *value*  
 Designa el valor devuelto por el *código*. *Value* es un parámetro necesario que llama a para un valor de entrada de *código* 0x0001, 0x0002 o 0x0003.  
  
> [!NOTE]  
>  Un valor de *código* de 2 es un tipo de datos de cadena. Cualquier otra entrada de valor de *código* o devuelta por *valor* es un entero.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El parámetro *Value* puede devolver uno de los siguientes valores de *código* .  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 El parámetro *Value* devuelve uno de los siguientes valores de SCROLLOPT.  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 El parámetro *Value* devuelve uno de los siguientes valores de CCOPT.  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 o 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
