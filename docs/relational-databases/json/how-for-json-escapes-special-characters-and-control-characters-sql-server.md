---
title: "Cómo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control (SQL Server) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 02544dc43daaf3bc56ad78126b37c6653a770bda
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>Cómo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo la cláusula **FOR JSON** de una instrucción **SELECT** de SQL Server inserta caracteres de escape en caracteres especiales y representa caracteres de control en la salida JSON.  

> [!IMPORTANT]
> En esta página se describe la compatibilidad integrada con JSON en Microsoft SQL Server. Para obtener información general sobre la inserción de caracteres de escape y la codificación en JSON, vea la sección 2.5 de JSON RFC: [http://www.ietf.org/rfc/rfc4627.txt](http://www.ietf.org/rfc/rfc4627.txt).

## <a name="escaping-of-special-characters"></a>Secuencia de caracteres de escape en los caracteres especiales  
Si los datos de origen contienen caracteres especiales, la cláusula **FOR JSON** inserta caracteres de escape en ellos en la salida de JSON con `\`, tal y como se muestra en la tabla siguiente. Esta secuencia de escape se produce tanto en los nombres de propiedades como en sus valores.  
  
|**Carácter especial**|**Salida con escape**|  
|---------------------------|--------------------------|  
|Comillas (")|\\"|  
|Barra diagonal inversa (\\)|\\\|  
|Barra diagonal (/)|\\/|  
|Retroceso|\b|  
|Avance de página|\f|  
|Nueva línea|\n|  
|Retorno de carro|\r|  
|Tabulación horizontal|\t|  
  
## <a name="control-characters"></a>Caracteres de control  
Si los datos de origen contienen caracteres de control, la cláusula **FOR JSON** los codifica en la salida de JSON en formato `\u<code>`, tal y como se muestra en la tabla siguiente.  
  
|**Carácter de control**|**Salida codificada**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>Ejemplo  
 Se trata de un ejemplo de la salida de **FOR JSON** en datos de origen que incluye caracteres especiales y caracteres de control.  
  
 Consulta:  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 Resultado:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Más información sobre la compatibilidad integrada de JSON en SQL Server  
Para obtener una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte las [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en Azure SQL Database ofrecidas por el director de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[Cláusula FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
