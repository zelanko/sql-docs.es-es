---
title: Configurar las propiedades generales de un informe (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], properties
- properties [Reporting Services], general
ms.assetid: 10b941b2-28e6-4408-9ee4-acebc63c8496
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 23184e77efbe41eae3d4de434a30ff8f3a4847ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177035"
---
# <a name="configure-general-properties-for-a-report-report-manager"></a>Configurar las propiedades generales de un informe (Administrador de informes)
  
### <a name="to-configure-general-report-properties"></a>Para configurar las propiedades generales de un informe

1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md).

2.  En Administrador de informes, vaya a la página **contenido** . Navegue al informe cuyas propiedades generales desea configurar y ábralo.

3.  Haga clic en la pestaña **Propiedades**.

     O bien, si la página **contenido** está en la vista detalles, haga clic en el icono de la página de propiedades:

     ![Icono de la página de propiedades](media/prop.gif "Icono de la página de propiedades")

4.  Se muestra la página propiedades **generales** y puede configurar las propiedades de la siguiente manera:

    -   En la sección **propiedades** , puede modificar el nombre y la descripción del informe.

    -   Puede activar la casilla **ocultar en la vista de lista** para ocultar el elemento cuando se abre la página en el diseño de página predeterminado (vista de lista), que organiza los elementos en la página.

    -   En la sección **definición de informe** , haga clic en **Editar** para extraer una copia de la definición de informe. Las modificaciones que se realizan de manera local en la definición del informe no se guardan en el servidor de informes.

         O bien, para actualizar la definición de informe desde un archivo. RDL, haga clic en **Actualizar**.

        > [!NOTE]
        >  Si actualiza una definición de informe, debe restablecer la configuración del origen de datos cuando la actualización haya finalizado.

    -   Use los botones **eliminar** o **movimiento** para eliminar o cambiar el informe.

    -   También puede crear un informe vinculado.

5.  Cuando haya terminado de configurar las propiedades generales del informe, haga clic en **aplicar**.

## <a name="see-also"></a>Consulte también
 [Mueva o elimine un elemento &#40;administrador de informes página&#41;](report-server/move-or-delete-an-item-report-manager.md) [contenido &#40;administrador de informes](../../2014/reporting-services/contents-page-report-manager.md)&#41;[Buscar, ver y administrar informes &#40;generador de informes y SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) [Página propiedades generales, informes &#40;](../../2014/reporting-services/general-properties-page-reports-report-manager.md) administrador de informes&#41;


