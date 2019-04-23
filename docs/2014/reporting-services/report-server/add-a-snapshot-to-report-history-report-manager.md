---
title: Agregar una instantánea al historial de informes (Administrador de informes) | Microsoft Docs
ms.prod: reporting-services-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
helpviewer_keywords:
- report history [Reporting Services], adding snapshots
- historical data [Reporting Services]
- snapshots [Reporting Services], adding report snapshots
- adding snapshots to report history
- report snapshots [Reporting Services], adding
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 633ac335067f579459809264fb055ff43481f4e3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59935641"
---
# <a name="add-a-snapshot-to-report-history-report-manager"></a>Agregar una instantánea al historial de informes (Administrador de informes)

El historial de informes es un conjunto de instantáneas de informe que se crean a lo largo del tiempo. Una instantánea de informe es un informe que contiene información de diseño y resultados de consultas que se recuperaron en un momento concreto. A diferencia de los informes a petición, que obtienen resultados de consulta actualizados cuando se seleccionan, las instantáneas de informe se procesan según una programación y luego se guardan en un servidor de informes. Al seleccionar una instantánea de informe para su visualización, el servidor de informes recupera el informe almacenado en la base de datos del servidor de informes y muestra los datos y el diseño actualizados para el informe en el momento en que se creó la instantánea.  
  
Las instantáneas de informe no se guardan con un formato de representación concreto. En su lugar, las instantáneas de informe se representan en un formato de visualización final (como HTML) solo cuando un usuario o una aplicación lo solicita. La representación aplazada hace que las instantáneas sean portátiles. El informe se puede representar con el formato correcto para el dispositivo o explorador web que lo solicita.  
  
## <a name="to-manually-add-snapshots-to-report-history"></a>Para agregar manualmente instantáneas a un historial de informe

1. En el Administrador de informes, vaya a la página **Contenido** , desplace el puntero sobre el elemento del que quiere ver el historial y haga clic en la flecha de lista desplegable.
  
2. En el menú desplegable, haga clic en **Ver historial de informes**.  
  
3. Haga clic en **Nueva instantánea**. Se crea una nueva instantánea en la columna **Cuando se ejecuta** .  
  
    > [!NOTE]
    > Para ello, el administrador debe haber configurado el historial de informes con la opción **Permitir que el historial se cree manualmente**. Para obtener más información, vea [Limitar el historial de informe &#40;Administrador de informes&#41;](../reports/limit-report-history-report-manager.md).

4. Haga clic en **Aplicar**.

## <a name="to-automatically-add-all-snapshots-to-report-history"></a>Para agregar automáticamente todas las instantáneas al historial de informes  
  
1. Para un informe que ya está configurado para ejecutarse como una instantánea de ejecución de informes, puede establecer propiedades adicionales para guardar una copia de la instantánea en el historial del informe cada vez que se actualiza la instantánea.  
  
2. En el Administrador de informes, vaya a la página **Contenido** , desplace el puntero sobre el elemento del que quiere ver el historial y haga clic en la flecha de lista desplegable.  
  
3. En el menú desplegable, haga clic en **Administrar**.  
  
4. Haga clic en **Opciones de instantánea**.  
  
5. Active la casilla correspondiente a **Almacenar todas las instantáneas de ejecución de informes en el historial**.  
  
6. Haga clic en **Aplicar**.  
  
### <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>Para agregar automáticamente instantáneas al historial del informe basándose en una programación  
  
1. En el Administrador de informes, vaya a la página **Contenido** , desplace el puntero sobre el elemento del que quiere ver el historial y haga clic en la flecha de lista desplegable.  
  
2. En el menú desplegable, haga clic en **Administrar**.  
  
3. Haga clic en **Opciones de instantánea**.  
  
4. Active la casilla correspondiente a **Utilizar la siguiente programación para agregar instantáneas al historial de informe**. Realice una de las siguientes acciones:  
  
    - Seleccione **Programación específica del informe**. Rellene los detalles de la programación, seleccione las fechas de inicio y fin de la programación y, por último, haga clic en **Aceptar**.  
  
    - Seleccione **Programación compartida**. En la lista, seleccione la programación que prefiera.  
  
5. Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Vea también

- [Configurar las propiedades de ejecución de un informe &#40;el Administrador de informes&#41;](../reports/configure-execution-properties-for-a-report-report-manager.md)
- [Abrir y cerrar un informe &#40;Administrador de informes&#41;](../reports/open-and-close-a-report-report-manager.md)
- [Limitar el historial de informe &#40;Administrador de informes&#41;](../reports/limit-report-history-report-manager.md)
- [Programaciones](../subscriptions/schedules.md)   
- [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)