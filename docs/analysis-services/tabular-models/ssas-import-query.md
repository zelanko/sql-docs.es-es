---
title: Importar datos mediante una consulta nativa (Analysis Services) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 67466abfccb03a689d5f717159e833143fcfafb4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472061"
---
# <a name="import-data-by-using-a-native-query"></a>Importar datos usando una consulta nativa
[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]
Para los modelos tabulares 1400, la nueva experiencia de obtener datos en proyectos de Visual Studio Analysis Services proporciona gran flexibilidad en cómo puede mashup sus datos durante la importación. Este artículo describe la creación de una conexión a un origen de datos y, a continuación, crear una consulta SQL nativa para especificar la importación de datos.

Para completar las tareas descritas en este artículo, asegúrese de que usa la versión más reciente de SSDT. Si usa Visual Studio 2017, asegúrese de que ha descargado e instalado la septiembre de 2017 o posterior Microsoft Analysis Services proyectos VSIX.

[Descargar e instalar SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Descargar Microsoft Analysis Services proyectos VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>Crear una conexión de origen de datos
Si ya no tiene una conexión a su origen de datos, deberá crear uno.

1. En Visual Studio > **Explorador de modelos tabulares**, haga clic en **orígenes de datos**y, a continuación, haga clic en **nuevo origen de datos**.
2. En **obtener datos**, seleccione el tipo de origen de datos y, a continuación, haga clic en **Connect**. Siga los pasos adicionales necesarios para conectarse a su origen de datos.


## <a name="enter-a-query-as-a-named-expression"></a>Escriba una consulta como una expresión con nombre
1. En **Explorador de modelos tabulares**, haga clic en **expresiones** > **editar expresiones**.
2. En **Editor de consultas**, haga clic en **consulta** > **nueva consulta** > **consulta en blanco**
3. En la barra de fórmulas, escriba
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM ...")
    ```
4. Para crear una tabla, en **consultas**, haga clic en la consulta y, a continuación, seleccione **crear nueva tabla**. La nueva tabla tendrá el mismo nombre que la consulta.


## <a name="example"></a>Ejemplo
Esta consulta nativa, crea una tabla de empleados en el modelo que incluye todas las columnas de la tabla Dimension.Employee en el origen de datos.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![Editor de consultas](media/ssas-import-query-example.png)


Después de importar, se crea una tabla denominada a empleados en el modelo.   

![Editor de consultas](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>Vea también  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [Suplantación](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
