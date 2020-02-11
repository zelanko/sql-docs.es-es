---
title: Página nueva suscripción o editar suscripción (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e02d6529-ce67-4305-b7f0-433997e99c21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 968362b2835c0e76f2a44c44e6cd427af863e8e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108142"
---
# <a name="new-subscription-or-edit-subscription-page-report-manager"></a>Página Nueva suscripción o Editar suscripción (Administrador de informes)
  Use la página Nueva suscripción o Editar suscripción para crear una nueva suscripción a un informe o modificar una existente. Las opciones de esta página varían dependiendo de los roles que tenga asignados. Los usuarios con permisos avanzados pueden trabajar con más opciones.  
  
 Las suscripciones se admiten para informes que se pueden ejecutar en modo desatendido. Como mínimo, el informe debe usar credenciales almacenadas o ninguna credencial. Si el informe utiliza parámetros, debe especificarse un valor predeterminado. Las suscripciones pueden pasar a estar inactivas si se cambia la configuración de ejecución del informe o si se quitan los valores predeterminados que se utilizan en las propiedades de los parámetros. Para obtener más información, vea [crear y administrar suscripciones para servidores de informes en modo nativo](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md).  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-new-subscription-or-edit-subscription-page"></a>Para abrir la página Nueva suscripción o Editar suscripción  
  
1.  Abra el Administrador de informes y busque el informe para el que desea agregar una suscripción.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, siga uno de estos procedimientos:  
  
    -   Haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe. A continuación, seleccione la pestaña **suscripciones** . En la barra de herramientas, haga clic en **nueva suscripción**o seleccione una suscripción existente y haga clic en **Editar**.  
  
    -   Haga clic en **Suscribir**. Se abrirá la página **Nueva suscripción** para el informe.  
  
## <a name="options"></a>Opciones  
 **Entregado por**  
 Seleccione la extensión de entrega que se va a utilizar para distribuir el informe. Según la extensión de entrega que usted seleccione, aparece la siguiente configuración:  
  
-   Las suscripciones de correo electrónico proporcionan campos que resultan familiares a los usuarios de correo electrónico (por ejemplo, los campos **para**, **asunto**y **prioridad** ). Especifique **Incluir informe** para incrustar o adjuntar el informe, o **Incluir vínculo** , para incluir una dirección URL en el informe. Especifique **Formato de representación** para elegir un formato de presentación para el informe que ha adjuntado o incrustado.  
  
-   La suscripción a recursos compartidos de archivos proporciona campos que permiten especificar una ubicación de destino. Puede entregar cualquier informe a un recurso compartido de archivos. Sin embargo, los informes que admiten características interactivas, como los informes matriciales que permiten obtener detalles de filas y columnas complementarias, se representan como archivos estáticos. En este tipo de archivos, no es posible ver filas y columnas de detalle. El nombre del recurso compartido de archivos debe especificarse en el formato UNC (Convención de nomenclatura universal \\) (por ejemplo, \mycomputer\public\myreportfiles). No incluya una barra inversa al final del nombre de la ruta de acceso. El archivo del informe se entregará en un formato de archivo basado en el formato de representación (por ejemplo, si elige **Excel**, el informe se entrega como archivo .xls).  
  
 La disponibilidad de una extensión de entrega depende de si está instalada y configurada en el servidor de informes. El correo electrónico del Servidor de informes es la extensión de entrega predeterminada, pero debe configurarla primero para poder utilizarla. No es necesario configurar la entrega al recurso compartido de archivos, pero se debe definir una carpeta compartida para poder utilizarla.  
  
## <a name="subscription-processing-options"></a>Opciones de procesamiento de suscripciones  
 Use estas opciones para definir las condiciones que hacen que se procese una suscripción. Algunas de ellas solo están disponibles para los informes que utilizan parámetros o que se ejecutan como instantáneas de ejecución de informes.  
  
 **Cuando se actualiza el contenido del informe**  
 Seleccione esta opción para suscribirse a una instantánea de informe que se actualiza según una programación. Esta opción solo está visible si se suscribe a un informe que se ejecuta como instantánea de ejecución de informes. Normalmente, el contenido de una instantánea de ejecución de informes se actualiza según una programación. Para los informes que se ejecutan en este modo, puede definir una suscripción que se realice cuando se actualice la instantánea.  
  
 **Cuando termina la ejecución del informe programado**  
 Cree una programación que determine cuándo se procesa la suscripción.  
  
 **En una programación compartida**  
 Seleccione una programación predefinida para procesar la suscripción.  
  
 **Escribir valores de parámetro**  
 Use esta opción cuando vaya a suscribirse a un informe que tiene parámetros. Esta opción solo está disponible para los informes con parámetros. Cuando se suscriba a un informe con parámetros, puede especificar los valores de parámetros que se utilizan para crear la versión del informe que se entrega a través de la suscripción. Por ejemplo, puede especificar un código de región para seleccionar los datos de ventas de una región determinada. Si no especifica ningún valor, se utiliza el valor predeterminado.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar un servidor de informes para la entrega por correo electrónico &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Crear, modificar y eliminar programaciones](subscriptions/create-modify-and-delete-schedules.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
