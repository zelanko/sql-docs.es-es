---
title: 'Lección tutorial de Analysis Services 13: implementar | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ed155c0d3621c59e844e30d10dc7117e587a8f9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="deploy"></a>Implementar

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, configurará propiedades de implementación; especificar un servidor para implementar en y un nombre para el modelo. A continuación, implementar el modelo en el servidor. Después de implementa el modelo, los usuarios pueden conectarse a él mediante el uso de una aplicación de cliente de informes. Para obtener más información, consulte [implementar en Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) y [implementación de la solución de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 12: analizar en Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Si la implementación en Azure Analysis Services, debe tener [permisos de administrador](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) en el serever.  

> [!IMPORTANT]  
> Si instaló la base de datos de ejemplo AdventureWorksDW en un servidor local de SQL, y va a implementar el modelo a un servidor de Analysis Services de Azure, un [puerta de enlace de datos local](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) es necesario.
  
## <a name="deploy-the-model"></a>Implementar el modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propiedades de implementación  

  
1.  En **el Explorador de soluciones**, haga clic en el **AW Internet Sales** del proyecto y, a continuación, haga clic en **propiedades**.  
  
2.  En el **páginas de propiedades de ventas de Internet de AW** cuadro de diálogo **el servidor de implementación**, en la **Server** propiedad, escriba el nombre completo del servidor. Si se conecta a Analysis Services de Azure, nombre del servidor debe incluir la dirección URL completa.

    ![como-lesson13--propiedades de implementación](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  En el **base de datos** propiedad, escriba **Adventure Works Internet Sales**.  
  
4.  En el **nombre del modelo** propiedad, escriba **Adventure Works Internet Sales Model**.  
  
5.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Para implementar Adventure Works Internet Sales
  
1.  En **el Explorador de soluciones**, haga clic en el **AW Internet Sales** proyecto > **generar**.  

2.  Haga clic en el **AW Internet Sales** proyecto > **implementar**.

    Cuando se implementa en Azure Analysis Services, se le pedirá que especifique su cuenta. Escriba su cuenta profesional y la contraseña, por ejemplo nancy@adventureworks.com. Esta cuenta debe ser de administradores en el servidor.
  
    El cuadro de diálogo implementar aparece y muestra el estado de implementación de los metadatos y cada tabla incluida en el modelo.  
    
    ![como-lesson13-implementar-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. Cuando se complete correctamente la implementación, continúe y haga clic en **Cerrar**.  
  

En esta lección se describe el método más común y sencillo para implementar un modelo tabular desde SSDT. Opciones de implementación avanzada, como el Asistente para la implementación o automatizar con XMLA y AMO proporcionan mayor flexibilidad, la coherencia y las implementaciones programadas. Para obtener más información, consulte [implementación de la solución de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).

## <a name="conclusion"></a>Conclusión  
¡Enhorabuena! Haya terminado de crear e implementar el primer modelo Tabular de Analysis Services. Este tutorial le ha guiado por las tareas más comunes para crear un modelo tabular. Ahora que su modelo Ventas por Internet de Adventure Works está implementado, puede utilizar el SQL Server Management Studio para administrarlo, crear scripts de proceso y realizar un plan de copia de seguridad. Los usuarios ahora también pueden conectarse al modelo mediante una aplicación de cliente de informes como Microsoft Excel o Power BI.  

![ssms como lesson13](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>¿Qué sigue?
[Conectar con Power BI Desktop](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[Lección complementaria - seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[Lección complementaria - filas de detalles](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[Lección complementaria - jerarquías desiguales](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
