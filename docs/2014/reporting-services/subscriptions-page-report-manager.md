---
title: Página suscripciones (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: cf3a6bd0-e0b2-4875-a532-63ef34cfa860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec92d7c58b68b14374666f65489f145fa863422
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101086"
---
# <a name="subscriptions-page-report-manager"></a>Suscripciones (página del Administrador de informes)
  Use la página Suscripciones para mostrar todas las suscripciones del informe u origen de datos compartido actual. Si tiene permisos suficientes, concedidos por la tarea "Administrar todas las suscripciones", puede ver las suscripciones de todos los usuarios. En caso contrario, esta página solo muestra las suscripciones que le pertenecen.  
  
> [!NOTE]  
>  Otras páginas contienen también información acerca de las suscripciones. Para obtener más información, consulte la [página Mis suscripciones &#40;Administrador de informes&#41;](../../2014/reporting-services/my-subscriptions-page-report-manager.md) para tener acceso a todas las suscripciones en un solo lugar o la [página nueva suscripción o editar suscripción &#40;administrador de informes&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md) para crear o editar una suscripción.  
  
 Algunas opciones solo se mostrarán si hay suscripciones con las que trabajar. Si no se han definido suscripciones y ha obtenido acceso a esta página desde un informe, las únicas opciones de la página serán **Nueva suscripción** y **Nueva suscripción controlada por datos** .  
  
 Para poder crear una suscripción nueva, debe comprobar primero si el origen de datos de informe usa credenciales almacenadas. Use la página de propiedades Orígenes de datos para almacenar las credenciales. Para obtener más información, vea [Página de propiedades orígenes de datos &#40;Administrador de informes&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md).  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-subscriptions-page-for-report"></a>Para abrir la página Suscripciones para el informe  
  
1.  Abra el Administrador de informes y busque el informe del que desea ver o configurar una suscripción.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe.  
  
4.  Seleccione la pestaña **Suscripciones** .  
  
## <a name="options"></a>Opciones  
 **Eliminar**  
 Haga clic para eliminar una suscripción. Para poder eliminar suscripciones, debe activar la casilla situada junto a cada suscripción que desee eliminar.  
  
 **Nueva suscripción**  
 Haga clic para crear una nueva suscripción al informe actual. Este botón se habilita si el informe no usa credenciales o usa credenciales almacenadas. No está disponible si abre la página Suscripciones para un origen de datos compartido.  
  
 **Nueva suscripción controlada por datos**  
 Haga clic para generar una lista de suscriptores y opciones de entrega ejecutando un comando o una consulta en un almacén de datos que contenga esa información. Este botón se habilita si el informe no usa credenciales o usa credenciales almacenadas. No está disponible si abre la página Suscripciones para un origen de datos compartido.  
  
 **Edición**  
 Haga clic para ver o editar la descripción.  
  
 **Informe**  
 Cuando se abre esta página desde un origen de datos compartido, esta columna identifica el informe para el que se ha definido la suscripción. La columna **Carpeta** identifica la ubicación del informe.  
  
 **Descripción**  
 Muestra una descripción de la suscripción.  
  
 **Desencadenador**  
 Identifica los criterios que hacen que se ejecute la suscripción. El desencadenador **TimedSubscription** se basa en una programación que define cuándo se ejecuta la suscripción. El desencadenador **SnapshotUpdated** se basa en la actualización de una instantánea de informe.  
  
 **Propietario**  
 Muestra el nombre del usuario que creó la suscripción.  
  
 **Última ejecución**  
 Muestra la última vez que se procesó la suscripción.  
  
 **Estado**  
 Muestra el estado de la suscripción. Por lo general, el valor de estado es Nuevo o la fecha y hora en la que se ejecutó por última vez la suscripción.  
  
 El valor de estado "Datos no válidos" se produce cuando la suscripción incluye un puntero para valores cifrados que ya no son válidos (es decir, a las credenciales almacenadas utilizadas para ejecutar el informe). Los valores cifrados existentes se convierten en inutilizables cuando se vuelven a crear las claves simétricas utilizadas para cifrar y descifrar datos en el servidor de informes.  
  
 No se puede procesar una suscripción si se ha desactivado. Para actualizar la suscripción y hacer que sea operativa, ábrala y guárdela.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Crear, modificar y eliminar suscripciones estándar &#40;Reporting Services en modo nativo&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Crear, modificar y eliminar programaciones](subscriptions/create-modify-and-delete-schedules.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
