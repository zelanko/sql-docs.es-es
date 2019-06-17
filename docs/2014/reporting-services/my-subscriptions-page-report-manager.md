---
title: Página Mis suscripciones (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 491a85a3-f323-4155-a0a8-de2779899995
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 75d662f677ee2b6bbab8e445804ca7f142b5c034
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108190"
---
# <a name="my-subscriptions-page-report-manager"></a>Mis suscripciones (página del Administrador de informes)
  Use la página Mis suscripciones para ver todas sus suscripciones en un solo lugar. Desde esta página, puede obtener acceso a cualquier suscripción de su propiedad, modificarla o eliminarla. Es propietario solamente de las suscripciones que ha creado. No puede obtener acceso a las suscripciones de otros usuarios, ni siquiera aunque las utilice (por ejemplo, si se ha agregado su nombre a una suscripción existente definida por otro usuario). Desde esta página no se pueden crear suscripciones. Para obtener más información sobre cómo crear suscripciones, vea el [página nueva suscripción o Editar suscripción &#40;el Administrador de informes&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md).  
  
 De manera predeterminada, las suscripciones se ordenan alfabéticamente por nombre de informe. Haga clic en un encabezado de columna diferente para cambiar el orden de las suscripciones. Si no tiene suscripciones o si el permiso para crear o administrar suscripciones está deshabilitado, no aparecen suscripciones en la página.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-my-subscriptions-page"></a>Para abrir la página Mis suscripciones  
  
1.  Abra el Administrador de informes.  
  
2.  En la esquina superior derecha, haga clic en Mis suscripciones.  
  
    > [!NOTE]  
    >  La opción Mis suscripciones siempre está disponible, aunque no tenga permisos para crear suscripciones.  
  
## <a name="options"></a>Opciones  
 **Eliminar**  
 Active la casilla situada al lado de cada suscripción que desee eliminar y haga clic en **Eliminar**.  
  
 **Editar**  
 Haga clic para ver o editar la descripción.  
  
 **Informe**  
 Muestra el informe especificado en la suscripción. Haga clic en el nombre del informe para verlo.  
  
 **Descripción**  
 Muestra una descripción de la suscripción. Haga clic en la descripción para ver o editar la información de suscripción del informe.  
  
 **Carpeta**  
 Muestra la carpeta que contiene el informe especificado en la suscripción. Haga clic en el nombre de la carpeta para ver su contenido.  
  
 **Desencadenador**  
 Identifica los criterios que hacen que se ejecute la suscripción. El desencadenador **TimedSubscription** se basa en una programación que define cuándo se ejecuta la suscripción. El desencadenador **SnapshotUpdated** se basa en la actualización de una instantánea de informe.  
  
 **Última ejecución**  
 Muestra la última vez que se procesó la suscripción.  
  
 **Estado**  
 Muestra el estado de la suscripción. Normalmente, el valor de estado es "Nueva" o contiene la fecha y la hora de la última vez que se ejecutó la suscripción.  
  
 El valor de estado "Datos no válidos" se produce cuando la suscripción incluye un puntero para valores cifrados que ya no son válidos (es decir, a las credenciales almacenadas utilizadas para ejecutar el informe). Los valores cifrados existentes se convierten en inutilizables cuando se vuelven a crear las claves simétricas utilizadas para cifrar y descifrar datos en el servidor de informes.  
  
 No se puede procesar una suscripción si se ha desactivado. Para actualizar la suscripción y hacer que sea operativa, ábrala y guárdela.  
  
## <a name="see-also"></a>Vea también  
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
