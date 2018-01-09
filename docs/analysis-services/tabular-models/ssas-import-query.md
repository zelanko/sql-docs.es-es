---
title: Importar datos mediante una consulta nativa (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 10/26/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b1200775d4b80639c3e6e2cb5ab127e3d1bb5254
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="import-data-by-using-a-native-query"></a>Importar datos mediante una consulta nativa
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Para los modelos tabulares 1400, la nueva experiencia de obtener datos en proyectos de Visual Studio Analysis Services proporciona una gran flexibilidad en cómo se puede mezclar los datos durante la importación. Este artículo describe la creación de una conexión a un origen de datos y, a continuación, crear una consulta SQL nativa para especificar la importación de datos.

Para completar las tareas descritas en este artículo, asegúrese de que está utilizando la versión más reciente de SSDT. Si usa Visual Studio de 2017, asegúrese de que se ha descargado e instalado la de 2017 septiembre o posterior Microsoft Analysis Services proyectos VSIX.

[Descargue e instale SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Descargar proyectos de Microsoft Analysis Services VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>Crear una conexión de origen de datos
Si ya no tiene una conexión a su origen de datos, debe crear uno.

1. En Visual Studio > **Explorador de modelos tabulares**, haga clic en **orígenes de datos**y, a continuación, haga clic en **nuevo origen de datos**.
2. En **obtener datos**, seleccione el tipo de origen de datos y, a continuación, haga clic en **conectar**. Siga los pasos adicionales necesarios para conectarse a su origen de datos.


## <a name="enter-a-query-as-a-named-expression"></a>Escriba una consulta como una expresión con nombre
1. En **Explorador de modelos tabulares**, haga clic en **expresiones** > **editar expresiones**.
2. En **Editor de consultas**, haga clic en **consulta** > **nueva consulta** > **consulta en blanco**
3. En la barra de fórmulas, escriba
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM …")
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

  
