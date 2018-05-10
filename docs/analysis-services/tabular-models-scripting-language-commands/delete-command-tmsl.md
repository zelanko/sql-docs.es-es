---
title: Eliminar comando (TMSL) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7f5338616b9020534e2b8fc45a80dcd577c49505
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="delete-command-tmsl"></a>Eliminar comando (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Elimina una base de datos o un objeto en la base de datos actual.   
Elimina el objeto especificado y todas las colecciones y los objetos secundarios. Si el objeto no existe, el comando genera un error.  
  
## <a name="request"></a>Solicitud  
 El objeto que se va a eliminar se especifica mediante la ruta de acceso del objeto. Por ejemplo, al eliminar una partición requiere que especifique los objetos de base de datos y la tabla que lo preceden.  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "table": "Reseller Sales",   
      "partition": "may2011"   
    }   
  }   
}   
```  
  
 Puede eliminar los siguientes objetos:  
  
 [Objeto de base de datos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016"  
    }   
  }   
}   
```  
  
 [Objeto de orígenes de datos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)  
  
```  
{  
  "delete": {  
    "object": {  
      "database": "AdventureworksDW2016",  
      "dataSource": "SqlServer localhost AdventureworksDW2016"  
    }  
  }  
}  
```  
  
 [Tables, objeto &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "table": "Reseller Sales",  
    }   
  }   
}   
```  
  
 [Objeto de particiones &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "table": "Reseller Sales",   
      "partition": "may2011"   
    }   
  }   
}   
```  
  
 [Objeto de los roles &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "role": "Data Reader"  
    }   
  }   
}   
```  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="examples"></a>Ejemplos  
 **Ejemplo 1** : eliminar una base de datos.  
  
```  
{  
  "delete": {  
    "object": {  
      "database": "AdventureWorksDW2016"  
    }  
  }  
}  
```  
  
 **Ejemplo 2** : eliminar una conexión.  
  
```  
{  
  "delete": {  
    "object": {  
      "database": "AdventureWorksDW2016",  
      "dataSource": "SqlServer localhost AdventureworksDW2016"  
    }  
  }  
}  
```  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS.  Por ejemplo, haga clic en una base de datos > **Script** > **base de datos de secuencia de comandos como** > **DELETE To**.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema [Tabular Model Scripting Language &#40;TMSL&#41; referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para obtener información sobre lo que es compatible.  

## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
