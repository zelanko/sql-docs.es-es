---
title: Limpiar datos mediante conocimiento (externo) de datos de referencia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 158009e9-8069-4741-8085-c14a5518d3fc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e35d5ae9390a6b316ec41ce20a2983c1c78a1696
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62793271"
---
# <a name="cleanse-data-using-reference-data-external-knowledge"></a>Limpiar datos mediante conocimiento (externo) de datos de referencia
  En este tema se describe cómo limpiar los datos utilizando el conocimiento de los proveedores de datos de referencia. Aunque los pasos que se siguen para limpiar los datos mediante el conocimiento de los proveedores de datos de referencia son los mismos que los que se usan en la ejecución de una actividad de limpieza, tal como se explica en [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md), en este tema se proporciona información específica para la limpieza de datos mediante el servicio de datos de referencia de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
 Cuando se utiliza la característica de servicio de datos de referencia en DQS para limpiar los datos, el proceso de limpieza de DQS envía los valores de dominio asignados al proveedor del servicio de datos de referencia en forma de solicitud de procesamiento por lotes. El servicio de datos de referencia responde con la información siguiente:  
  
-   Corrección sugerida  
  
-   Confianza  
  
-   Información adicional sobre el dominio asignado. Los datos de referencia también pueden normalizar, analizar o enriquecer el origen con datos adicionales. Esta información se proporciona en campos adicionales de la respuesta.  
  
 Después de obtener la respuesta del servicio de datos de referencia, en DQS ocurre lo siguiente durante la actividad de limpieza:  
  
-   Dependiendo de los valores especificados para **Umbral de corrección automática** y **Confianza mínima** durante la asignación de los dominios con el servicio de datos de referencia, los valores de dominio se corrigen o se sugieren automáticamente en función del nivel de confianza.  
  
    > [!NOTE]  
    >  Los valores de umbral que se aplican durante la limpieza de datos utilizando el conocimiento del servicio de datos de referencia son los especificados durante la asignación de un dominio a un servicio de datos de referencia, no los especificados en la pestaña **Configuración general** de la sección **Configuración** . Para obtener información acerca de cómo especificar los valores de umbral para la limpieza de datos de referencia, consulte el paso 9 de [adjuntar un dominio o un dominio compuesto a datos de referencia](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
-   Los valores de dominio se clasifican en las siguientes categorías: **Sugerido**, **Nuevo**, **No válido**, **Corregido** y **Correcto**.  
  
-   Los datos adicionales se anexan al origen, y la información, junto con los datos limpios, está disponible para su exportación.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Debe haber asignado los dominios requeridos de una base de conocimiento de DQS al servicio de datos de referencia apropiado. Además, la base de conocimiento debe contener conocimiento sobre el tipo de datos que desea limpiar. Por ejemplo, si quiere limpiar los datos de origen que contienen direcciones de EE. UU., debe asignar los dominios a un proveedor de servicios de datos de referencia que proporcione datos de alta calidad para esas direcciones. Para obtener más información, consulte [adjuntar un dominio o un dominio compuesto a datos de referencia](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_kb_operator en la base de datos DQS_MAIN para realizar la limpieza de datos.  
  
##  <a name="Cleanse"></a> Limpiar los datos mediante el conocimiento de los datos de referencia  
 Continuaremos con el mismo ejemplo del uso de los dominios que asignamos en el tema anterior, [adjuntar un dominio o un dominio compuesto a datos de referencia](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md), con el servicio Melissa Data de Windows Azure Marketplace. Ahora, utilizaremos los mismos dominios para limpiar algunas direcciones de EE. UU. de ejemplo. Los pasos necesarios para limpiar los datos son los mismos que los que se describen en [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md). Sin embargo, requeriremos su atención siempre que sea necesario durante el proceso.  
  
1.  Cree un proyecto de calidad de datos y seleccione la actividad **Limpieza** . Consulte [Create a Data Quality Project](../../2014/data-quality-services/create-a-data-quality-project.md).  
  
2.  En la página **Asignar**, asigne los siguientes cuatro dominios a las columnas correspondientes en los datos de origen: **Línea de dirección**, **Ciudad**, **Estado** y **Código postal**. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Como ha asignado los cuatro dominios dentro del dominio compuesto **Address Verification** , la limpieza de datos ahora se realizará en el nivel de dominio compuesto, y no en el nivel de dominio individual.  
  
3.  En la página **Limpieza** , ejecute el proceso de limpieza asistido por PC haciendo clic en **Iniciar**. Una vez finalizado el proceso de limpieza, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  En la página **Limpieza** , DQS muestra información sobre los dominios adjuntados al servicio de datos de referencia de estas dos formas:  
    >   
    >  -   Se muestra un mensaje debajo del botón **Iniciar**: "Dominios \<Dominio1>, \<Dominio2>… \<DominioN> se limpian mediante el proveedor de servicios de datos al que se hace referencia". En este ejemplo, se mostrará el mensaje siguiente: "La verificación de dirección de dominio se limpia mediante el proveedor de servicios de datos de referencia".  
    > -   Se mostrará el icono ![El dominio se ha adjuntado al servicio de datos remotos (RDS)](../../2014/data-quality-services/media/dqs-rdsindicator.JPG "El dominio se ha adjuntado al servicio de datos remotos (RDS)") en el área **Generador de perfiles** para los dominios adjuntados al proveedor de servicios de datos de referencia. En este ejemplo, el icono se mostrará en el dominio compuesto **Address Verification** .  
  
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
  
     ![Limpieza mediante el servicio de datos de referencia](../../2014/data-quality-services/media/dqs-rdscleansing.JPG "Limpieza mediante el servicio de datos de referencia")  
  
    > [!NOTE]  
    >  En los dominios compuestos, DQS también resalta en otro color los dominios individuales que se corrigieron durante el proceso de limpieza asistido por PC. Por ejemplo, en este caso, los dominios **Address line** y **State** se corrigieron y, por consiguiente, se han resaltado en cian.  
  
5.  Después de que finalice la revisión de todos los valores de dominio, haga clic en **Siguiente** para exportar los datos.  
  
6.  En la página **Exportar** , observará que además de la información habitual acerca de la actividad de limpieza para cada dominio (Origen, Motivo, Confianza y Estado), existe información adicional proporcionada por el servicio de datos de referencia Melissa Data sobre los datos de la dirección, como la latitud y la longitud de esta, el nombre del condado, el tipo de dirección (edificio, calle, etc.), y otros.  
  
7.  Exporte los datos al destino requerido (SQL Server, CSV o Excel) y haga clic en **Finalizar** para cerrar el proyecto.  
  
    > [!IMPORTANT]  
    >  Si utiliza la versión de 64 bits de Excel, no puede exportar los datos limpiados en un archivo de Excel; puede exportar únicamente a una base de datos de SQL Server o un archivo .csv.  
  
  
