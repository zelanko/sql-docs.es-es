---
title: sp_cursoroption (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b404bdb0b96883df1b1e39b9190285b4795aeaa4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240045"
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece las opciones de cursor o devuelve información del cursor creada mediante el procedimiento almacenado sp_cursoropen. sp_cursoroption se invoca especificando el identificador = 8 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Es un *controlar* valor generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y devuelto por el procedimiento almacenado sp_cursoropen. *cursor* requiere un **int** valor para la ejecución de entrada.  
  
 *Código*  
 Se usa para estipular varios factores de los valores devueltos del cursor. *código* requiere uno de los siguientes **int** valores de entrada:  
  
|Value|Nombre|Description|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|Devuelve el puntero de texto y no los datos reales, para ciertas columnas de imagen o texto designado.<br /><br /> TEXTPTR_ONLY permite punteros de texto que se usará como *identificadores* para objetos blob que posteriormente se pueden recuperar de forma selectiva o actualizan utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)] o DBLIB (p. ej. [!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT o DBLIB DBWRITETEXT).<br /><br /> Si se asigna el valor "0", todas las columnas de imagen y texto de la lista de selección devolverán punteros de texto en lugar de datos.|  
|0x0002|CURSOR_NAME|Asigna el nombre especificado en *valor* hasta el cursor. Esto, a su vez, permite a ODBC utilizar [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones UPDATE o DELETE posicionadas en los cursores abiertos a través de sp_cursoropen.<br /><br /> La cadena se puede especificar como cualquier tipo de datos Unicode o de caracteres.<br /><br /> Puesto que [!INCLUDE[tsql](../../includes/tsql-md.md)] las instrucciones UPDATE o DELETE posicionadas funcionan de forma predeterminada, en la primera fila de un cursor grueso, sp_cursor SETPOSITION se debería utilizar para colocar el cursor antes de emitir la instrucción UPDATE o DELETE posicionada.|  
|0x0003|TEXTDATA|Devuelve los datos reales, no el puntero de texto, para ciertas columnas de imagen o texto en las capturas siguientes (es decir, se deshace el efecto de TEXTPTR_ONLY).<br /><br /> Si TEXTDATA está habilitado para una columna en particular, la fila se vuelve a capturar o actualizar, y puede establecerse a continuación de nuevo en TEXTPTR_ONLY. Como con TEXTPTR_ONLY, el parámetro de valor es un entero que especifica el número de columnas y un valor cero devuelve todas las columnas de texto o imagen.|  
|0x0004|SCROLLOPT|Opción de desplazamiento. Vea "Valores del código de retorno", posteriormente en este tema, para obtener información adicional.|  
|0x0005|CCOPT|Opción de control de simultaneidad. Vea "Valores del código de retorno", posteriormente en este tema, para obtener información adicional.|  
|0x0006|ROWCOUNT|El número de filas que están actualmente en el conjunto de resultados.<br /><br /> Nota: El recuento de filas puede haber cambiado el valor devuelve sp_cursoropen, si se utiliza el rellenado asincrónico. Se devuelve el valor -1 si se desconoce el número de filas.|  
  
 *value*  
 Designa el valor devuelto por *código*. *valor* es un parámetro necesario que requiere un 0 x 0001, 0 x 0002 o 0 x 0003 *código* valor de entrada.  
  
> [!NOTE]  
>  A *código* valor 2 es un tipo de datos de cadena. Cualquier otro *código* valor de entrada o devuelto por *valor* es un entero.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El *valor* parámetro puede devolver uno de los siguientes *código* valores.  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 El *valor* parámetro devuelve uno de los siguientes valores SCROLLOPT.  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 El *valor* parámetro devuelve uno de los siguientes valores CCOPT.  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 o 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
