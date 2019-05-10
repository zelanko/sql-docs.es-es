---
title: 'Lección 13: Implementar | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c20a0367612aee48c1a58e9cde8ba1a44d3fafc
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404807"
---
# <a name="lesson-13-deploy"></a>Lección 13: Implementar
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, configurará propiedades de implementación; especificar una local o instancia de servidor de Azure y un nombre para el modelo. A continuación, implementará el modelo a esa instancia. Después de implementa el modelo, los usuarios pueden conectarse a él mediante el uso de una aplicación cliente de informes. Para más información acerca de la implementación, consulte [implementación de la solución de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md) y [implementar en Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 12: Analizar en Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Implementar el modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propiedades de implementación  
  
1.  En **el Explorador de soluciones**, haga clic en el **AW Internet Sales** del proyecto y, a continuación, haga clic en **propiedades**.  
  
2.  En el **AW Internet Sales Property Pages** cuadro de diálogo **servidor de implementación**, en el **Server** propiedad, escriba el nombre de un servidor de Azure Analysis Services o un instancia del servidor local que se ejecuta en modo Tabular. Se trata de la instancia del servidor al que se va a implementar el modelo.  

    ![aas-deploy-deployment-server-property](media/aas-deploy-deployment-server-property.png)
 
    > [!IMPORTANT]  
    > Debe tener permisos de administrador en el remoto Analysis Services instancia poder implementar en él.  
  
3.  En el **base de datos** propiedad, tipo **Adventure Works Internet Sales**.  
  
4.  En el **Model Name** propiedad, tipo **Adventure Works Internet Sales Model**.  
  
5.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Para implementar el modelo tabular Ventas por Internet de Adventure Works  
  
1.  En **el Explorador de soluciones**, haga clic en el **AW Internet Sales** proyecto > **compilar**.  

2.  Haga clic en el **AW Internet Sales** proyecto > **implementar**.

    Al implementar en Azure Analysis Services, es probable que se le pedirá que escriba su contraseña. Escriba su cuenta profesional y contraseña, por ejemplo nancy@adventureworks.com. Esta cuenta debe estar en administradores en la instancia del servidor.
  
    Aparece el cuadro de diálogo Implementar en el que se muestra el estado de implementación de los metadatos y las tablas incluidas en el modelo.  
    
    ![aas-deploy-status](media/aas-deploy-status.png)
  
3. Cuando se complete correctamente la implementación, continúe y haga clic en **Cerrar**.  
  
## <a name="conclusion"></a>Conclusión  
¡Enhorabuena! Ha terminado de crear e implementar su primer modelo Tabular de Analysis Services. Este tutorial le ha guiado por las tareas más comunes para crear un modelo tabular. Ahora que su modelo Ventas por Internet de Adventure Works está implementado, puede utilizar el SQL Server Management Studio para administrarlo, crear scripts de proceso y realizar un plan de copia de seguridad. Los usuarios ahora también pueden conectarse al modelo mediante una aplicación cliente de informes como Microsoft Excel o Power BI.  

![as-tabular-lesson13-ssms](media/as-tabular-lesson13-ssms.png)
  
  
## <a name="see-also"></a>Vea también  
[Modo DirectQuery](../tabular-models/directquery-mode-ssas-tabular.md)  
[Configurar las propiedades predeterminadas de modelado de datos y de implementación](../tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[Bases de datos de modelo tabular](../tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  ## <a name="whats-next"></a>¿Qué sigue?
*  [Lección complementaria: implementar seguridad dinámica utilizando filtros de fila](supplemental-lesson-implement-dynamic-security-by-using-row-filters.md).

*  [Complementario lección: configurar propiedades de informes para informes de Power View](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md).
