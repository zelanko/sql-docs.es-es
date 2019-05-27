---
title: Almacenar en caché un conjunto de datos compartido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c759eaf0fd18709e09eb64da6bfeb2d66a69f595
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104257"
---
# <a name="cache-a-shared-dataset"></a>Almacenar en caché un conjunto de datos compartido
  Una manera de mejorar el rendimiento es configurar las propiedades de almacenamiento en caché para un conjunto de datos compartido. Cuando un conjunto de datos compartido se almacena en memoria caché, se guarda una copia de los resultados de la consulta durante un breve período de tiempo. El primer usuario que solicite un informe que utilice el conjunto de datos compartido debe esperar a que los resultados de la consulta y todo el procesamiento se completen antes de ver el informe. Los usuarios subsiguientes que solicitan el informe dentro del período de almacenamiento en caché experimentarán mejor rendimiento porque la consulta y el procesamiento ya se han producido. También puede especificar un plan de actualización de la memoria caché para ejecutar la consulta y almacenar en memoria caché los resultados hasta que expire la memoria caché especificada.  
  
 Los usuarios que ejecutan informes basados en un conjunto de datos compartido o los planes de actualización de la memoria caché crean la memoria caché de consulta y, en ambos casos, la memoria caché está disponible en función de sus opciones de expiración.  
  
 Hay restricciones en los tipos de conjuntos de datos compartidos que puede almacenar en memoria caché. Por ejemplo, los resultados de la consulta no pueden estar almacenados en memoria caché si los datos varían en función de la identidad del usuario o si los datos se recuperan usando el token de seguridad del usuario que solicita el informe. Para más información, vea [Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](cache-shared-datasets-ssrs.md) e [Informes almacenados en caché &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Para programar la expiración de un informe en caché  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue al conjunto de datos compartidos para el que desea establecer propiedades de almacenamiento en caché, mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**.  
  
4.  En el marco de la izquierda, haga clic en la pestaña **Almacenando en caché**.  
  
    > [!NOTE]  
    >  Si ve el error **Las credenciales usadas para ejecutar este conjunto de datos compartidos no están almacenadas**, la opción Almacenar en caché conjunto de datos compartido se deshabilitará. Tiene que modificar el origen de datos para almacenar las credenciales o modificar el conjunto de datos compartido para utilizar un origen de datos diferente que almacene las credenciales.  
  
5.  Seleccione **Almacenar en caché conjunto de datos compartido**.  
  
6.  Seleccione la opción para que la memoria caché expire después de 30 minutos. También puede elegir que la memoria caché expire en una programación especificada.  
  
7.  Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Vea también  
 [Administración de conjuntos de datos compartidos](../report-data/manage-shared-datasets.md)  
  
  
