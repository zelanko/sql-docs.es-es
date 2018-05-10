---
title: Crear una alerta de datos en el Diseñador de alertas de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8464ab9d-afe1-4490-955f-9f3319bcbf8d
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 10f7e6d3f3ea4da0b9c7bb285c87c414bd1df58f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-data-alert-in-data-alert-designer"></a>Crear una alerta de datos en el Diseñador de alertas de datos

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Las definiciones de alertas de datos se crean en el Diseñador de alertas de datos. Una vez guardadas las definiciones de alertas, es posible volver a abrirlas, modificarlas y volver a guardarlas en el Diseñador de alertas de datos. Para más información sobre cómo editar definiciones de alertas, vea [Administrar mis alertas de datos en el Administrador de alertas de datos](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md) y [Editar una alerta de datos en el Diseñador de alertas](../reporting-services/edit-a-data-alert-in-alert-designer.md).

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

## <a name="create-a-data-alert-definition"></a>Crear una definición de alerta de datos
 
1.  Busque la biblioteca de SharePoint que contiene el informe para el que desea crear una definición de alerta de datos.  
  
2.  Haga clic en el informe.  
  
     El informe se ejecuta. Si el informe tiene parámetros, compruebe que el informe muestra los datos para los que desea recibir mensajes de alerta. Si no ve las columnas o los valores que le interesan, puede que desee volver a ejecutar el informe con valores de parámetros diferentes.  
  
    > [!NOTE]  
    >  Los valores de parámetro que eligió para ejecutar el informe se guardan en la definición de alerta y se usarán cuando se vuelva a ejecutar el informe durante el procesamiento de la definición de alerta. Para utilizar valores de parámetro diferentes, debe crear una nueva definición de alerta.  
  
3.  En el menú **Acciones** , haga clic en **Nueva alerta de datos**.  
  
     La imagen siguiente muestra el menú **Acciones** .  
  
     ![Abrir el Diseñador de alertas desde la biblioteca de SharePoint](../reporting-services/media/rs-openalertdesigneriw.gif "Abrir el Diseñador de alertas desde la biblioteca de SharePoint")  
  
     Se abre el Diseñador de alertas de datos y en él se muestra una tabla con las 100 primeras filas de la primera fuente de distribución de datos generada por el informe.  
  
    > [!NOTE]  
    >  Si no ve la opción **Nueva alerta de datos** , el servicio de alertas no está configurado en el sitio de SharePoint o la edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no incluye alertas de datos. Para más información, vea [Aplicaciones de servicio y servicio de SharePoint de Reporting Services](../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
    >   
    >  Si la opción **Nueva alerta de datos** aparece atenuada, el origen de datos del informe está configurado para utilizar las credenciales de seguridad integradas o para solicitar credenciales. Para que la opción **Nueva alerta de datos** esté disponible, debe actualizar el origen de datos de modo que use las credenciales almacenadas o no use credenciales.  
  
     El nombre de la fuente de distribución de datos aparece en la lista desplegable **Nombre de los datos de informe** .  
  
4.  De manera opcional, seleccione otra fuente de distribución de datos en la lista desplegable **Nombre de los datos de informe** .  
  
     Si no se genera ninguna fuente de distribución de datos a partir del informe, no puede crear una definición de alerta para el informe. El diseño del informe determina el contenido de cada fuente de distribución de datos. Para más información, vea [Generar fuentes de distribución de datos a partir de informes &#40;Generador de informes y SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
5.  Si lo desea, en el cuadro de texto **Nombre de alerta** , cambie el nombre predeterminado por otro más significativo.  
  
     El nombre predeterminado de la definición de alerta es el nombre del informe. Los nombres de definición de alertas no tienen que ser únicos, lo que puede dificultar distinguirlos al ver la lista de alertas posteriormente en el Administrador de alertas de datos. Se recomienda que utilice nombres significativos y únicos para sus definiciones de alerta.  
  
6.  Si lo desea, cambie la opción de datos predeterminada de **algún dato de la fuente de distribución de datos tiene** a **ningún dato de la fuente de distribución de datos tiene**.  
  
7.  Haga clic en **Agregar regla**.  
  
     Aparece una lista de columnas en la fuente de distribución de datos.  
  
8.  En la lista, seleccione la columna que desee utilizar en la regla y, a continuación, seleccione un operador de comparación y escriba el valor del umbral.  
  
     Se muestran distintos operadores de comparación en función del tipo de datos de la columna seleccionada. Si la columna tiene un tipo de datos de fecha, se muestra un icono de calendario junto al valor del umbral de la regla. Puede especificar una fecha haciendo clic en una fecha en el calendario o escribiendo la fecha.  
  
     El Diseñador de alertas de datos proporciona dos modos de comparación: **Modo de entrada de valores** y **Modo de selección de campos**. El modo predeterminado es **Modo de entrada de valores**. Solo puede agregar cláusulas OR cuando se encuentre en el **Modo de entrada de valores** y utilice la comparación **is** .  
  
9. Para agregar una cláusula OR, haga clic en la flecha abajo y, después, haga clic en **Modo de entrada de valores**.  
  
10. Escriba el valor de comparación.  
  
11. De manera opcional, vuelva a hacer clic en el signo de puntos suspensivos **(…)** .  
  
     Los puntos suspensivos **(…)** aparecen en la línea que contiene la primera cláusula.  
  
     La cláusula OR se agrega debajo y dentro de la regla AND.  
  
12. De manera opcional, haga clic en la flecha abajo, seleccione **Modo de selección de campos**y, después, seleccione una columna de la lista.  
  
     Observará que el signo de puntos suspensivos **(…)** en los que se hace clic para agregar cláusulas OR ha desaparecido.  
  
13. Si lo desea, haga clic en **Agregar regla** de nuevo para agregar más reglas.  
  
     Las reglas se combinan mediante el operador lógico AND.  
  
14. Seleccione una opción en la lista de periodicidad. Dependiendo del tipo de periodicidad, especifique un intervalo.  
  
15. Si lo desea, haga clic en **Avanzadas**.  
  
16. Si lo desea, cambie la fecha en que se inicia el mensaje de alerta escribiendo otra fecha o abriendo el calendario y haciendo clic en una fecha en el mismo.  
  
     La fecha de inicio predeterminada es la fecha actual.  
  
17. Si lo desea, active la casilla situada junto a **Detener alerta el**y después elija una fecha para detener el mensaje de alerta.  
  
     De forma predeterminada, un mensaje de alerta no tiene ninguna fecha de detención.  
  
    > [!NOTE]  
    >  La detención de un mensaje de alerta no elimina la definición de alerta. Después de detener un mensaje de alerta, puede reiniciarlo actualizando las fechas de inicio y detención. Para más información sobre cómo eliminar definiciones de alertas, vea [Administrar mis alertas de datos en el Administrador de alertas de datos](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
18. Si lo desea, desactive la casilla **Enviar mensaje solo si cambian los resultados** .  
  
     Si envía mensajes de alerta con frecuencia, la información redundante puede que no sea del agrado de todos y debería desactivar esta casilla.  
  
19. Escriba las direcciones de correo electrónico de los destinatarios del mensaje de alerta. Separe las direcciones con signos de punto y coma.  
  
     Si la dirección de correo electrónico de la persona que ha creado la definición de alerta está disponible, se agrega al cuadro **Destinatarios** .  
  
20. Si lo desea, en el cuadro de texto **Asunto** , actualice la línea de asunto del mensaje de alerta.  
  
     El asunto predeterminado es **Alerta de datos para \<nombre de alerta>**.  
  
21. Si lo desea, en el cuadro de texto **Descripción** , escriba una descripción del mensaje de alerta.  
  
22. Haga clic en **Guardar**.  

## <a name="see-also"></a>Ver también

[Diseñador de alertas de datos](../reporting-services/data-alert-designer.md)   
[Administrador de alertas de datos para administradores de alertas](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Alertas de datos de Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
