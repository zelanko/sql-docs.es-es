---
title: "Almacenar en caché un conjunto de datos compartido | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b80d9627570c00b68fd0728377053f4bba6b2031
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="cache-a-shared-dataset"></a>Almacenar en caché un conjunto de datos compartido
  Una manera de mejorar el rendimiento es configurar las propiedades de almacenamiento en caché para un conjunto de datos compartido. Cuando un conjunto de datos compartido se almacena en memoria caché, se guarda una copia de los resultados de la consulta durante un breve período de tiempo. El primer usuario que solicite un informe que utilice el conjunto de datos compartido debe esperar a que los resultados de la consulta y todo el procesamiento se completen antes de ver el informe. Los usuarios subsiguientes que solicitan el informe dentro del período de almacenamiento en caché experimentarán mejor rendimiento porque la consulta y el procesamiento ya se han producido. También puede especificar un plan de actualización de la memoria caché para ejecutar la consulta y almacenar en memoria caché los resultados hasta que expire la memoria caché especificada.  
  
 Los usuarios que ejecutan informes basados en un conjunto de datos compartido o los planes de actualización de la memoria caché crean la memoria caché de consulta y, en ambos casos, la memoria caché está disponible en función de sus opciones de expiración.  
  
 Hay restricciones en los tipos de conjuntos de datos compartidos que puede almacenar en memoria caché. Por ejemplo, los resultados de la consulta no pueden estar almacenados en memoria caché si los datos varían en función de la identidad del usuario o si los datos se recuperan usando el token de seguridad del usuario que solicita el informe. Para más información, vea [Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md) e [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Para programar la expiración de un informe en caché  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, navegue al conjunto de datos compartidos para el que desea establecer propiedades de almacenamiento en caché, mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**.  
  
4.  En el marco de la izquierda, haga clic en la pestaña **Almacenando en caché**.  
  
    > [!NOTE]  
    >  Si ve el error **Las credenciales usadas para ejecutar este conjunto de datos compartidos no están almacenadas**, la opción Almacenar en caché conjunto de datos compartido se deshabilitará. Tiene que modificar el origen de datos para almacenar las credenciales o modificar el conjunto de datos compartido para utilizar un origen de datos diferente que almacene las credenciales.  
  
5.  Seleccione **Almacenar en caché conjunto de datos compartido**.  
  
6.  Seleccione la opción para que la memoria caché expire después de 30 minutos. También puede elegir que la memoria caché expire en una programación especificada.  
  
7.  Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Vea también  
 [Administrar conjuntos de datos compartidos](../../reporting-services/report-data/manage-shared-datasets.md)  
  
  
