---
title: "Limpiar datos mediante conocimiento (externo) de datos de referencia | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 158009e9-8069-4741-8085-c14a5518d3fc
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# Limpiar datos mediante conocimiento (externo) de datos de referencia
  En este tema se describe cómo limpiar los datos utilizando el conocimiento de los proveedores de datos de referencia. Mientras todos los pasos de la ejecución de una actividad de limpieza sigue siendo la misma para limpiar los datos mediante el conocimiento de los proveedores de datos de referencia como se explica en el [Limpiar datos usando DQS & #40; interno & #41; Conocimiento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md), este tema proporciona información específica para la limpieza de datos mediante el servicio de datos de referencia en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
 Cuando se utiliza la característica de servicio de datos de referencia en DQS para limpiar los datos, el proceso de limpieza de DQS envía los valores de dominio asignados al proveedor del servicio de datos de referencia en forma de solicitud de procesamiento por lotes. El servicio de datos de referencia responde con la información siguiente:  
  
-   Corrección sugerida  
  
-   Confianza  
  
-   Información adicional sobre el dominio asignado. Los datos de referencia también pueden normalizar, analizar o enriquecer el origen con datos adicionales. Esta información se proporciona en campos adicionales de la respuesta.  
  
 Después de obtener la respuesta del servicio de datos de referencia, en DQS ocurre lo siguiente durante la actividad de limpieza:  
  
-   Dependiendo de los valores especificados para **Umbral de corrección automática** y **Confianza mínima** durante la asignación de los dominios con el servicio de datos de referencia, los valores de dominio se corrigen o se sugieren automáticamente en función del nivel de confianza.  
  
    > [!NOTE]  
    >  Los valores de umbral que se aplican durante la limpieza de datos utilizando el conocimiento del servicio de datos de referencia son los especificados durante la asignación de un dominio a un servicio de datos de referencia, no los especificados en la pestaña **Configuración general** de la sección **Configuración** . Para obtener información acerca de cómo especificar valores de umbral para la limpieza de datos de referencia, consulte el paso 9 de [adjuntar dominio o dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
-   Los valores de dominio se clasifican en las categorías siguientes: **Sugerido**, **Nuevo**, **No válido**, **Corregido**y **Correcto**.  
  
-   Los datos adicionales se anexan al origen, y la información, junto con los datos limpios, está disponible para su exportación.  
  
## Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Debe haber asignado los dominios requeridos de una base de conocimiento de DQS al servicio de datos de referencia apropiado. Además, la base de conocimiento debe contener conocimiento sobre el tipo de datos que desea limpiar. Por ejemplo, si desea limpiar los datos de origen que contienen direcciones de EE. UU., debe asignar los dominios a un proveedor de servicios de datos de referencia que proporcione datos de alta calidad para dichas direcciones. Para obtener más información, consulte [adjuntar dominio o dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_kb_operator en la base de datos DQS_MAIN para realizar la limpieza de datos.  
  
##  <a name="Cleanse"></a> Limpiar los datos mediante el conocimiento de los datos de referencia  
 Continuaremos con el mismo ejemplo del uso de los dominios que asignamos en el tema anterior, [adjuntar dominio o dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md), con el servicio Melissa Data en Windows Azure Marketplace. Ahora, utilizaremos los mismos dominios para limpiar algunas direcciones de EE. UU. de ejemplo. Los pasos para limpiar los datos son los mismos que se describe en [Limpiar datos usando DQS & #40; interno & #41; Conocimiento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md). Sin embargo, requeriremos su atención siempre que sea necesario durante el proceso.  
  
1.  Cree un proyecto de calidad de datos y seleccione la actividad **Limpieza** . Consulte [Create a Data Quality Project](../data-quality-services/create-a-data-quality-project.md).  
  
2.  En la página **Asignación** , asigne los 4 dominios siguientes a las columnas apropiadas de los datos de origen: **Address Line**, **City**, **State**y **Zip**. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Como ha asignado todos los 4 dominios la **Address Verification** dominio compuesto, la limpieza de datos ahora se llevará a cabo en el nivel de dominio compuesto y no en el nivel de dominio individual.  
  
3.  En el **Cleanse** página, ejecute el proceso de limpieza asistida por PC haciendo clic en **iniciar**. Una vez finalizado el proceso de limpieza, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  En el **Cleanse** página, DQS muestra información sobre los dominios que se adjuntan a la referencia de servicio de datos en los siguientes dos maneras:  
    >   
    >  -   Se muestra un mensaje debajo de la **iniciar** botón: "dominios \< Dominio1>, \< dominio2>,... \< Dominion> se limpian mediante el proveedor de servicios de datos de referencia. " En este ejemplo, se mostrará el siguiente mensaje: “El dominio Access Verification se limpia mediante el proveedor de servicios de datos al que se hace referencia”.  
    > -   Un icono, ![El dominio se ha adjuntado al servicio de datos remotos (RDS)](../data-quality-services/media/dqs-rdsindicator.png "El dominio se ha adjuntado al servicio de datos remotos (RDS)"), se muestra en el **Profiler** área con los dominios conectados al proveedor de servicios de datos de referencia. En este ejemplo, el icono se mostrará en el dominio compuesto **Address Verification** .  
  
4.  En la página **Administrar y ver resultados** , revise los valores de dominio. El servicio de datos de referencia puede mostrar varias sugerencias, si están disponibles, para un valor dependiendo del número máximo de sugerencias especificadas en el cuadro **Candidatos sugeridos** durante la asignación del dominio al servicio de datos de referencia. Por ejemplo, se muestran dos sugerencias para la dirección de EE. UU. siguiente:  
  
     **Valor original:**  
  
    |Address Line|City|State|Zip|  
    |------------------|----------|-----------|---------|  
    |1 msft way|Redmond||98052|  
  
     **Valores sugeridos:**  
  
    |Address Line|City|State|Zip|  
    |------------------|----------|-----------|---------|  
    |1 Microsoft Way|Redmond|WA|98052|  
    |PO BOX 1|Redmond|WA|98073|  
  
     ![Limpieza mediante servicio de datos de referencia](../data-quality-services/media/dqs-rdscleansing.JPG "Limpieza mediante servicio de datos de referencia")  
  
    > [!NOTE]  
    >  En los dominios compuestos, DQS también resalta en otro color los dominios individuales que se corrigieron durante el proceso de limpieza asistido por PC. Por ejemplo, en este caso, los dominios **Address line** y **State** se corrigieron y, por consiguiente, se han resaltado en cian.  
  
5.  Después de que finalice la revisión de todos los valores de dominio, haga clic en **Siguiente** para exportar los datos.  
  
6.  En el **exportar** página, observará que además de la información habitual acerca de la actividad de limpieza para cada dominio (origen, motivo, confianza y estado), no hay información adicional proporcionada por la referencia de Melissa Data service datos acerca de los datos de dirección, como la latitud y longitud de la dirección, el nombre de la provincia, la dirección, escriba (highrise, calle, etc.) y así sucesivamente.  
  
7.  Exportar los datos al destino requerido (SQL Server, CSV o Excel) y haga clic en **Finalizar** para cerrar el proyecto.  
  
    > [!IMPORTANT]  
    >  Si utiliza la versión de 64 bits de Excel, no puede exportar los datos limpiados en un archivo de Excel; puede exportar únicamente a una base de datos de SQL Server o un archivo .csv.  
  
  