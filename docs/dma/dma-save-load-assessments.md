---
title: Guardar y cargar evaluaciones con Data Migration Assistant
description: Aprenda a usar Data Migration Assistant para guardar y cargar evaluaciones.
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 02a6d49202ad2607d862246eee232e599788244a
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885862"
---
# <a name="save-and-load-assessments-with-data-migration-assistant"></a>Guardar y cargar evaluaciones con Data Migration Assistant

Las siguientes instrucciones paso a paso le ayudarán a usar el Data Migration Assistant v 5.0 o posterior para guardar una evaluación de base de datos en un archivo y, a continuación, cargar una evaluación desde un archivo.

> [!NOTE]
> Además de cargar las evaluaciones guardadas con la versión más reciente de DMA, los usuarios también pueden aprovechar esta característica para cargar las evaluaciones exportadas como archivos. JSON de versiones anteriores de Data Migration Assistant para ver los resultados en v 5.0 y versiones posteriores.

## <a name="saving-an-assessment-to-a-file"></a>Guardar una evaluación en un archivo

1. Después de ejecutar una evaluación mediante Data Migration Assistant, seleccione **Guardar evaluación**.

   ![Abrir el cuadro de diálogo Guardar evaluación](../dma/media/dma-save-load-assessments/dma-open-save-dialog.png)

   El estándar **Guardar..** . aparecerá el cuadro de diálogo.

   > [!NOTE]
   > Para obtener más información sobre cómo ejecutar una evaluación en Data Migration Assistant, consulte el artículo [realización de una evaluación de SQL Server migración con Data Migration Assistant](../dma/dma-assesssqlonprem.md).

2. Especifique un nombre para el archivo y, a continuación, seleccione **Guardar**.

   ![Nombrar y guardar un archivo de evaluación](../dma/media/dma-save-load-assessments/dma-name-save-assessment.png)

## <a name="loading-an-assessment-saved-to-a-file"></a>Carga de una evaluación guardada en un archivo

1. Para cargar una evaluación que haya guardado previamente en un archivo, inicie Data Migration Assistant y, a continuación, en la pestaña **todas las evaluaciones** , seleccione **evaluación de carga**.

   ![Abrir el cuadro de diálogo evaluación de carga](../dma/media/dma-save-load-assessments/dma-open-load-dialog.png)

2. Navegue hasta el archivo de evaluación guardado que desea cargar, seleccione el archivo y, a continuación, seleccione **abrir**.

   ![Apertura de un archivo de evaluación](../dma/media/dma-save-load-assessments/dma-open-assessment.png)

   Aparecerá una entrada para la evaluación que cargó en la pestaña **todas las evaluaciones** .

   ![Mostrando entrada de evaluación](../dma/media/dma-save-load-assessments/dma-display-assessment-entry.png)

3. Seleccione la entrada evaluación y, a continuación, seleccione **abrir evaluación**.

   ![Abrir los detalles de la evaluación](../dma/media/dma-save-load-assessments/dma-open-assessment-detail.png)

   En Data Migration Assistant ahora se muestran los detalles de la evaluación que se había ejecutado anteriormente.

   ![Mostrar detalles de la evaluación](../dma/media/dma-save-load-assessments/dma-display-assessment-detail.png)
