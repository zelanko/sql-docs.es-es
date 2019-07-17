---
title: 'Analysis Services lección 13 del tutorial: Implementar | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 4e8e6bea11794545a2b0ab9c340e85344ec23d33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162214"
---
# <a name="deploy"></a>Implementar

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, configurará propiedades de implementación; especificación de un servidor para implementar en y un nombre para el modelo. A continuación, implementar el modelo en el servidor. Después de implementa el modelo, los usuarios pueden conectarse a él mediante el uso de una aplicación cliente de informes. Para obtener más información, consulte [implementar en Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) y [implementación de la solución de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 12: Analizar en Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Si la implementación en Azure Analysis Services, debe tener [permisos de administrador](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) en el serever.  

> [!IMPORTANT]  
> Si instaló la base de datos de ejemplo AdventureWorksDW en un servidor local SQL Server y a implementar el modelo a un servidor de Azure Analysis Services, un [puerta de enlace de datos local](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) es necesario.
  
## <a name="deploy-the-model"></a>Implementar el modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propiedades de implementación  

  
1.  En **el Explorador de soluciones**, haga clic en el **AW Internet Sales** del proyecto y, a continuación, haga clic en **propiedades**.  
  
2.  En el **AW Internet Sales Property Pages** cuadro de diálogo **servidor de implementación**, en el **Server** propiedad, escriba el nombre completo del servidor. Si se conecta a Azure Analysis Services, nombre del servidor debe incluir la dirección URL completa.

    ![as-lesson13-deploy-property](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  En el **base de datos** propiedad, tipo **Adventure Works Internet Sales**.  
  
4.  En el **Model Name** propiedad, tipo **Adventure Works Internet Sales Model**.  
  
5.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Para implementar las ventas por Internet de Adventure Works
  
1.  En **el Explorador de soluciones**, haga clic en el **AW Internet Sales** proyecto > **compilar**.  

2.  Haga clic en el **AW Internet Sales** proyecto > **implementar**.

    Al implementar en Azure Analysis Services, se le pedirá que escriba su contraseña. Escriba su cuenta profesional y contraseña, por ejemplo nancy@adventureworks.com. Esta cuenta debe estar en administradores en el servidor.
  
    Cuadro de diálogo implementar aparece y muestra el estado de implementación de los metadatos y cada tabla incluida en el modelo.  
    
    ![como-lesson13-implementar-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. Cuando se complete correctamente la implementación, continúe y haga clic en **Cerrar**.  
  

En esta lección se describe el método más común y sencillo para implementar un modelo tabular desde SSDT. Opciones de implementación avanzadas como el Asistente para la implementación o la automatización con XMLA y AMO proporcionan mayor flexibilidad, coherencia e implementaciones programadas. Para obtener más información, consulte [implementación de la solución de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).

## <a name="conclusion"></a>Conclusión  
¡Enhorabuena! Ha terminado de crear e implementar su primer modelo Tabular de Analysis Services. Este tutorial le ha guiado por las tareas más comunes para crear un modelo tabular. Ahora que su modelo Ventas por Internet de Adventure Works está implementado, puede utilizar el SQL Server Management Studio para administrarlo, crear scripts de proceso y realizar un plan de copia de seguridad. Los usuarios ahora también pueden conectarse al modelo mediante una aplicación cliente de informes como Microsoft Excel o Power BI.  

![as-lesson13-ssms](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>¿Qué sigue?
[Conectar con Power BI Desktop](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[Lección complementaria: seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[Lección complementaria: filas de detalles](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[Lección complementaria: jerarquías desiguales](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
