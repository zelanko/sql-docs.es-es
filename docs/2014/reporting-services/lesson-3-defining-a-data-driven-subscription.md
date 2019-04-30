---
title: 'Lección 3: Definir una suscripción controlada por datos | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eda13c16caf3f123887da00e2c7896d36b8bf7ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226028"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lección 3: Definir una suscripción controlada por datos
  En esta lección, utilizará las páginas de suscripción controladas por datos para conectar a un origen de datos de suscripción, crear una consulta que recupera datos de suscripción y asignar el conjunto de resultados a las opciones de informe y entrega.  
  
> [!NOTE]  
>  Antes de empezar, compruebe que el servicio del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esté en ejecución. Si no es así, no podrá guardar la suscripción.  
  
 En esta lección se supone que completó la lección 1 y la lección 2, y que el origen de datos del informe usa credenciales almacenadas.  Para obtener más información, vea [Lección 2: Modificar las propiedades del origen de datos de informe](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
 En este tema:  
  
-   [Iniciar al Asistente para la suscripción controlada por datos](#bkmk_startwizard)  
  
-   [Paso 1: definir una descripción](#bkmk_definesubscription)  
  
-   [Paso 2: definir una conexión al origen de datos de suscriptor](#bkmk_defineconnectiontosubscriber)  
  
-   [Paso 3: definir una consulta para recuperar datos del suscriptor](#bkmk_definequery)  
  
-   [Paso 4: establecer opciones de entrega](#bkmk_set_deliveryoptions)  
  
-   [Paso 5: configurar un valor de parámetro a la salida del informe muy](#bkmk_configure_parameter)  
  
-   [Paso 6: programar una suscripción](#bkmk_schedule_subscription)  
  
##  <a name="bkmk_startwizard"></a> Iniciar al Asistente para la suscripción controlada por datos  
  
1.  En el Administrador de informes, haga clic en **Inicio**y navegue hasta la carpeta que contiene el informe **Sales Orders** .  
  
2.  En el menú contextual del informe, haga clic en **Administrar**y, a continuación, haga clic en la pestaña **Suscripciones** .  
  
3.  Haga clic en **Nueva suscripción controlada por datos**. Si no ve este botón, no dispone de permisos para el Administrador de contenido.  
  
##  <a name="bkmk_definesubscription"></a> Paso 1: definir una descripción  
  
1.  Escriba **Entrega de pedido de ventas** en la descripción.  
  
2.  Seleccione **Windows FileShare** para **Especifique cómo se notifica a los destinatarios**.  
  
3.  Seleccione **Especifique solo esta suscripción**y, a continuación, haga clic en **Siguiente**.  
  
##  <a name="bkmk_defineconnectiontosubscriber"></a> Paso 2: definir una conexión al origen de datos de suscriptor  
  
1.  Seleccione **Microsoft SQL Server** como tipo de origen de datos.  
  
2.  En Cadena de conexión, escriba la siguiente cadena de conexión:  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  La base de datos de suscriptores se creó en la lección 1.  
  
3.  Haga clic en **Credenciales almacenadas de forma segura en el servidor de informes**.  
  
4.  En **Nombre de usuario** y **Contraseña**, escriba el nombre de usuario y la contraseña del dominio. Incluya tanto el dominio como la cuenta de usuario al especificar **Nombre de usuario**.  
  
    > [!NOTE]  
    >  Las credenciales usadas para conectarse a un origen de datos de suscriptor no se devuelven a [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Si modifica la suscripción más adelante, deberá volver a escribir la contraseña utilizada para conectarse al origen de datos.  
  
5.  Seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**y haga clic en **Siguiente**.  
  
##  <a name="bkmk_definequery"></a> Paso 3: definir una consulta para recuperar datos del suscriptor  
  
1.  En el cuadro de consultas, escriba la consulta siguiente:  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  Especifique un tiempo de espera de 30 segundos.  
  
3.  Haga clic en **Validar**y, a continuación, en **Siguiente**.  
  
##  <a name="bkmk_set_deliveryoptions"></a> Paso 4: establecer opciones de entrega  
  
1.  Como **Nombre de archivo**, seleccione **Obtener el valor de la base de datos**. Seleccione el campo **Order**.  
  
2.  En **Ruta de acceso**, seleccione **Especificar un valor estático**. En Valor de configuración, escriba el nombre de un recurso compartido de archivos público para el que disponga de permisos de escritura; por ejemplo, ( `\\mycomputer\public\myreports`).  
  
3.  En **Formato de representación**, seleccione **Obtener el valor de la base de datos**. Seleccione **Formato**.  
  
4.  Para el **Modo de escritura**, seleccione **Especificar un valor estático** y seleccione **Incrementar automáticamente**.  
  
5.  En **Extensión de archivo**, seleccione **Especificar un valor estático** y seleccione **True**.  
  
6.  En **Nombre de usuario**, seleccione **Especificar un valor estático**. Escriba su cuenta de usuario de dominio. Escríbalo en este formato: `<domain>\<account>`. La cuenta de usuario tiene que disponer de permisos en la ruta de acceso que configuró en los pasos anteriores.  
  
7.  En **Contraseña**, seleccione **Especificar un valor estático**. Escriba su contraseña. Escríbala con cuidado. El asistente no valida la contraseña.  
  
8.  Haga clic en **Siguiente.**  
  
##  <a name="bkmk_configure_parameter"></a> Paso 5: configurar un valor de parámetro a la salida del informe muy  
  
1.  En **OrderNumber**, seleccione **Obtener el valor de la base de datos**. En Valor, seleccione **Order**. Haga clic en **Siguiente.**  
  
##  <a name="bkmk_schedule_subscription"></a> Paso 6: programar una suscripción  
  
1.  Haga clic en **Según una programación creada para esta suscripción**y, a continuación, haga clic en **Siguiente**.  
  
2.  En **Detalles de programación**, haga clic en **Una vez**.  
  
3.  Especifique una hora de inicio que sea unos cuantos minutos después de la hora actual.  
  
4.  Haga clic en **Finalizar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Cuando se ejecute la suscripción, se entregarán cuatro archivos de informe al recurso compartido de archivos que ha especificado, uno por cada pedido del origen de datos *Subscribers* . Cada entrega debe ser única en cuanto a datos (los datos deben ser específicos de cada pedido), formato de representación y formato de archivo. Puede abrir cada informe desde la carpeta compartida para comprobar que todas las versiones se hayan personalizado en función de las opciones de suscripción que haya definido.  
  
 ![Lista de archivos creados por la suscripción](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "Lista de archivos creados por la suscripción")  
  
 La página de suscripción del Administrador de informes contendrá la fecha de **Última ejecución** y el **Estado** de la suscripción.  
  
> [!NOTE]  
>  Actualice la página cuando la suscripción se ejecute para ver la información actualizada.  
  
 ![Resultados de suscripción en el administrador de informes](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "Resultados de suscripción en el administrador de informes")  
  
 Con este paso finaliza el tutorial "Definir una suscripción controlada por datos". Para obtener más información sobre otros [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tutoriales, consulte [tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Crear, modificar y eliminar una suscripción controlada por datos](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [Usar un origen de datos externo para obtener información de los suscriptores &#40;suscripción controlada por datos&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
