---
title: ALTER, comando (TMSL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8bdc49f1-209e-4055-be19-c83862b81efa
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: da8bc8b79cf500686f7ce955132af426376f0a97
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="alter-command-tmsl"></a>Comando ALTER (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Modifica un objeto existente, pero no sus secundarios, en una instancia de Analysis Services en modo Tabular.  Si el objeto no existe, el comando genera un error.  
  
 Use **Alter** comando para las actualizaciones de destino, como establecer una propiedad en una tabla sin tener que especificar todas las columnas también. Este comando es similar a **CreateOrReplace**, pero sin necesidad de tener que proporcionar una definición de objeto completo.  
  
 Para objetos que tienen propiedades de lectura y escritura, si se especifica una propiedad de lectura y escritura, debe especificar todos ellos, con nueva o los valores existentes. Puede usar PowerShell de AMO para obtener una lista de propiedades. 
  
## <a name="request"></a>Solicitud  
 **ALTER** no tiene ningún atributo. Entradas incluyen el objeto que se va a modificar, seguido de la definición de objeto modificado.  
  
 En el ejemplo siguiente se muestra la sintaxis para cambiar una propiedad de un objeto de partición. La ruta de acceso de objeto establece qué partición de objeto es modificarse a través de pares de nombre-valor de los objetos primarios. La segunda entrada es un objeto de partición que especifica el nuevo valor de propiedad.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "\<database-name>",   
      "table": "\<table-name>",   
      "partition": "\<partition-name>"   
    },   
    "partition": {   
      "name": "\<new-partition-name>",   
       . . .  << other properties   
    }   
  }   
}   
```  
  
 La estructura de la solicitud varía según el objeto. **ALTER** puede utilizarse con cualquiera de los siguientes objetos:  
  
 [Objeto de base de datos &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) Cambiar el nombre de una base de datos.  
  
```  
"alter": {   
    "object": {   
      "database": "\<database-name>"  
    },   
    "database": {   
      "name": "\<new-database-name>",   
    }   
  }   
```  
  
 [Objeto de orígenes de datos &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) Cambiar el nombre de una conexión, que es un objeto secundario de la base de datos.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "dataSource":"SqlServer localhost AdventureworksDW2016"  
      },  
      "dataSource":{   
         "name":"A new connection name"  
      }  
   }  
}  
```  
  
 [Objeto de tablas &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Vea **ejemplo 1** a continuación.  
  
 [Objeto de particiones &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) Vea **ejemplo 2** a continuación.  
  
 [Objeto de roles &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) Cambiar una propiedad en un objeto de función.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "role":"DataReader"  
      },  
      "role":{   
         "name":"New Name"  
      }  
   }  
}  
```  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran la secuencia de comandos que puede ejecutar en una ventana XMLA en Management Studio o usar como entrada en [cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) en PowerShell de AMO.  
  
 **Ejemplo 1** -este script cambia la propiedad de nombre en una tabla.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "AdventureWorksDW2016",   
      "table": "DimDate"  
    },   
    "table": {   
      "name": "DimDate2"  
    }   
  }   
}  
```  
  
 Suponiendo que una instancia local con nombre (nombre de instancia es "tabular") y un archivo JSON con el script alter, este comando cambia el nombre de una tabla de DimDate a DimDate2:  
  
 `invoke-ascmd -inputfile '\\my-computer\my-shared-folder\altertablename.json' -server 'localhost\Tabular'`  
  
 **Ejemplo 2** --esta secuencia de comandos cambia el nombre de una partición, por ejemplo al final del año al año actual se convierte en el año anterior. Asegúrese de especificar todas las propiedades. Si deja **origen** no se especifica, podrían interrumpir todos de las definiciones de partición existente.  
  
 A menos que se va a crear, reemplazar, o modificar el propio objeto de origen de datos, cualquier origen de datos al que hace referencia en la secuencia de comandos (como en el siguiente script de partición) debe ser una existente **DataSource** objeto en el modelo. Si necesita cambiar el origen de datos, puede hacerlo como un paso independiente.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "InternetSales",   
      "table": "DimDate",  
      "partition": "CurrentYear"  
    },   
    "partition": {   
      "name": "Year2009",  
       "source": {  
             "query":  "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] WHERE [dbo].[DimDate].CalendarYear = 2009",  
              "dataSource": "SqlServer localhost AdventureworksDW2016"  
        }  
    }   
  }   
}  
```  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 No se puede generar un script listos para su uso para este comando de SSMS. En su lugar, puede comenzar con un ejemplo o escribir el suyo propio.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema ([Tabular Model Scripting Language &#40; TMSL &#41; Hacer referencia a](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para obtener información sobre lo que es compatible.  

## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
