---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: dce66e74f7415a8ff5ac6de4505d8a1f0632391b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108455"
---
# <a name="sp_cursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece las opciones de cursor o devuelve información del cursor creada por el sp_cursoropen procedimiento almacenado. sp_cursoroption se invoca especificando el identificador 8 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Es un valor de *identificador* generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y devuelto por el Sp_cursoropen procedimiento almacenado. el *cursor* requiere un valor de entrada **int** para la ejecución.  
  
 *codifica*  
 Se usa para estipular varios factores de los valores devueltos del cursor. el *código* requiere uno de los siguientes valores de entrada **int** :  
  
|Value|Nombre|Descripción|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|Devuelve el puntero de texto y no los datos reales, para ciertas columnas de imagen o texto designado.<br /><br /> TEXTPTR_ONLY permite usar punteros de texto como *identificadores* para objetos BLOB que se pueden recuperar o actualizar de forma selectiva mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] o con instalaciones de DBLIB ( [!INCLUDE[tsql](../../includes/tsql-md.md)] por ejemplo, READTEXT o DBLIB DBWRITETEXT).<br /><br /> Si se asigna el valor "0", todas las columnas de imagen y texto de la lista de selección devolverán punteros de texto en lugar de datos.|  
|0x0002|CURSOR_NAME|Asigna el nombre especificado en el *valor* al cursor. Esto, a su vez, permite a ODBC [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizar instrucciones UPDATE/DELETE posicionadas en cursores abiertos a través de Sp_cursoropen.<br /><br /> La cadena se puede especificar como cualquier tipo de datos Unicode o de caracteres.<br /><br /> Dado [!INCLUDE[tsql](../../includes/tsql-md.md)] que las instrucciones UPDATE/DELETE colocadas operan, de forma predeterminada, en la primera fila de un cursor FAT, se debe usar sp_cursor SETPOSITION para colocar el cursor antes de emitir la instrucción UPDATE/DELETE posicionada.|  
|0x0003|TEXTDATA|Devuelve los datos reales, no el puntero de texto, para ciertas columnas de imagen o texto en las capturas siguientes (es decir, se deshace el efecto de TEXTPTR_ONLY).<br /><br /> Si TEXTDATA está habilitado para una columna en particular, la fila se vuelve a capturar o actualizar, y puede establecerse a continuación de nuevo en TEXTPTR_ONLY. Como con TEXTPTR_ONLY, el parámetro de valor es un entero que especifica el número de columnas y un valor cero devuelve todas las columnas de texto o imagen.|  
|0x0004|SCROLLOPT|Opción de desplazamiento. Vea "Valores del código de retorno", posteriormente en este tema, para obtener información adicional.|  
|0x0005|CCOPT|Opción de control de simultaneidad. Vea "Valores del código de retorno", posteriormente en este tema, para obtener información adicional.|  
|0x0006|ROWCOUNT|El número de filas que están actualmente en el conjunto de resultados.<br /><br /> Nota: el recuento de filas puede haber cambiado desde el valor devuelto por sp_cursoropen si se utiliza el rellenado asincrónico. Se devuelve el valor-1 si se desconoce el número de filas.|  
  
 *valor*  
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
 [sp_cursor &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
