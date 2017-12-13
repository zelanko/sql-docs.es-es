---
title: "Crear una consulta de minería de datos utilizando XMLA | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: content queries [DMX]
ms.assetid: 8f6b6008-006c-4792-9bd1-64c30dc3fd41
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c2f5e3fd04ae0552ef9e8c7cae54e98bc7e46981
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>Crear una consulta de minería de datos utilizando XMLA
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Puede crear una variedad de consultas en objetos de minería de datos mediante AMO, DMX o XML/a.  
  
 XML se utiliza para la comunicación entre el servidor de Analysis Services y todos los clientes. Por consiguiente, aunque generalmente es mucho más fácil crear consultas de contenido utilizando DMX, puede escribirlas con las instrucciones COMMAND y DISCOVER de XML/A, con un cliente que admita el protocolo SOAP o creando una consulta XML/A en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 En este tema se explica cómo usar las plantillas XML/A disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear una consulta del contenido del modelo con un modelo de minería de datos almacenadas en el servidor actual.  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>Consultar conjuntos de filas de esquema de minería de datos utilizando XML/A  
  
#### <a name="to-open-an-xmla-template"></a>Para abrir una plantilla XML/A  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  Haga clic en el icono de cubo para abrir la lista de las plantillas de Analysis Services.  
  
3.  En la lista de categorías de plantilla, expanda **XMLA**, expanda **Conjuntos de filas de esquema**y haga doble clic en **Detectar conjuntos de filas de esquema** para abrir la plantilla en el editor de código adecuado.  
  
4.  En el cuadro de diálogo **Conectar a Analysis Services** , complete la información de conexión y, a continuación, haga clic en **Conectar**. Se abre una ventana nueva del editor de consultas, rellenada con la plantilla **Detectar conjuntos de filas de esquema** .  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>Para detectar los nombres de columna del conjunto de filas de esquema MINING MODEL CONTENT  
  
1.  Con la plantilla **Detectar conjuntos de filas de esquema** abierta, haga clic en **Ejecutar**.  
  
     En el panel **Resultados** se devuelve una lista de conjuntos de filas de esquema que contiene los nombres de los conjuntos de filas de esquema y las columnas de conjunto de filas para todos los conjuntos de filas disponibles en la instancia actual.  
  
2.  En el **consulta** panel, coloque el cursor después  **\<lista de restricciones >** y presione ENTRAR para agregar una nueva línea.  
  
3.  Coloque el cursor en la línea en blanco y escriba  **\<NombreDeEsquema > DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName >**  
  
     La sección completa para las restricciones debería aparecer de la forma siguiente:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  Haga clic en **Ejecutar**.  
  
     El panel **Resultados** muestra una lista de nombres de columna para el conjunto de filas de esquema especificado.  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>Para crear una consulta de contenido mediante el conjunto de filas de esquema MINING MODEL CONTENT  
  
1.  En la plantilla **Detectar conjuntos de filas de esquema** , cambie el tipo de solicitud reemplazando el texto dentro de las etiquetas de tipos de solicitud.  
  
     Reemplace esta línea:  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     con la siguiente:  
  
     **\<RequestType > DMSCHEMA_MINING_MODEL_CONTENT\</RequestType >**  
  
2.  Cambie la lista de restricciones para especificar un modelo de minería de datos por el nombre, agregando una condición nueva a las listas de restricciones.  
  
3.  En la plantilla, coloque el cursor después de `<Restriction List>` y presione Entrar para agregar una línea nueva.  
  
4.  Coloque el cursor en la línea en blanco y escriba **<MODEL_NAME>Nombre de mi modelo</MODEL_NAME>**.  
  
     La sección completa para las restricciones debería aparecer de la forma siguiente:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  Haga clic en **Ejecutar**.  
  
     El panel Resultados muestra la definición de esquema, junto con los valores para el modelo especificado.  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Conjuntos de filas de esquema de minería de datos](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
