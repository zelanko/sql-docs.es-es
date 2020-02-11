---
title: Página de propiedades opciones de instantánea (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f6641f59-5267-4f57-8957-63b93d1a9679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a73f3be75a7f0cadf633943aeafffb7217d8e29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101160"
---
# <a name="snapshot-options-properties-page-report-manager"></a>Página de propiedades de opciones de instantánea (Administrador de informes)
  Use la página de propiedades Opciones de instantánea para programar las instantáneas de informe que se van a agregar al historial del informe, y para establecer los límites del número de ellas que se almacenarán en el historial.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de, vea [servicios de base de datos adicionales](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md#Add_DBServices).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-snapshot-options-properties-page-for-a-report"></a>Para abrir la página de propiedades Opciones de instantánea de un informe  
  
1.  Abra el Administrador de informes y busque el informe para el que desea configurar las propiedades de la instantánea de informe.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe.  
  
4.  Seleccione la pestaña **Opciones de instantánea** .  
  
## <a name="options"></a>Opciones  
 **Permitir que el historial de informe se cree manualmente**  
 Active esta casilla para agregar instantáneas a un historial de informe según sea necesario. Al activarla, aparece el botón **Nueva instantánea** en la página Historial.  
  
 **Almacenar todas las instantáneas de ejecución de informes en el historial**  
 Active esta casilla para copiar en el historial de un informe una instantánea del informe generada según las propiedades de ejecución del informe. Puede establecer las propiedades de ejecución de informes para ejecutar un informe a partir de una instantánea generada. Al establecer esta propiedad del historial del informe, se puede mantener un registro de todas las instantáneas del informe generadas con el tiempo, colocando copias de las mismas en el historial.  
  
 **Utilizar la siguiente programación para agregar instantáneas al historial de informe**  
 Active esta casilla para agregar instantáneas al historial de un informe según una programación. Puede crear una programación exclusivamente con esta finalidad o seleccionar una programación compartida predefinida, si alguna contiene la información de programación que desea.  
  
 **Seleccione el número de instantáneas que desea mantener**  
 Seleccione alguna de las opciones siguientes para controlar el número de informes que desea guardar en el historial. La configuración de historial de informe puede variar para cada informe.  
  
-   Seleccione **Usar configuración predeterminada** para conservar la configuración predeterminada. El administrador del servidor de informes controla una configuración maestra para el almacenamiento de historial de informe. Si elige esta opción, el número de instantáneas guardadas se obtiene de esta configuración maestra.  
  
-   Seleccione **Conservar un número ilimitado de instantáneas en el historial de informe** para guardar todas las instantáneas del historial de informe. Para reducir el tamaño del historial de informe, debe eliminar las instantáneas manualmente.  
  
-   Seleccione **Limitar las copias del historial de informe** para guardar un número determinado de instantáneas. Cuando se alcanza el límite, las copias más antiguas se eliminan del historial de informe para dejar sitio para las nuevas.  
  
 El historial de informes está almacenado en la base de datos del servidor de informes. Si tiene informes grandes o numerosos informes para los que desea mantener el historial, piense en limitar la cantidad del historial del informe para ayudar a administrar las necesidades de espacio en disco de la base de datos del servidor de informes.  
  
 **Aplicar**  
 Haga clic para guardar los cambios.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar una instantánea al historial de informes &#40;Administrador de informes&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Crear, modificar y eliminar instantáneas del historial de informes](report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
