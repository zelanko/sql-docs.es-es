---
title: Utilizar el corrector ortográfico de DQS
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 65e4e53e-2699-4cae-a9e0-fe78547755b5
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 087d7c7636b456e9cba07eb16abdd135abb43c4e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257749"
---
# <a name="use-the-dqs-speller"></a>Utilizar el corrector ortográfico de DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  El corrector ortográfico de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) comprueba la sintaxis, la ortografía y la estructura de las frases de los valores de cadena de un dominio. El corrector ortográfico es una característica independiente, del lado cliente, que no se integra con los motores del servidor y no tiene ninguna implicación en los flujos o estados actuales. El corrector ortográfico identifica los valores de cadena que considera posibles errores, y los marca con un carácter de subrayado rojo en la misma ubicación en la que se realizan otros cambios manuales en los valores de dominio. Entre estas ubicaciones se incluyen:  
  
-   La página **Administrar valores del dominio** de la actividad **Detección de conocimiento**  
  
-   La página **Valores del dominio** o **Relaciones basadas en términos** de la actividad **Administración de dominios**  
  
-   La página **Administrar y ver resultados** de la actividad **Limpieza**  
  
 El corrector ortográfico solo funciona en dominios individuales con un tipo de datos de cadena. Todos los valores de un dominio individual del tipo de datos de cadena se envían al corrector ortográfico para su validación. El corrector ortográfico no funciona en los dominios compuestos, ni tampoco en aquellos con tipos distintos al de cadena, ni con valores mixtos (como letras y números sin espacio), numerales romanos, caracteres individuales y valores que constan únicamente de letras mayúsculas.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Para ejecutar el corrector ortográfico, es necesario tener una base de conocimiento y un dominio abiertos en la actividad Detección de conocimiento o Administración de dominios; además, es necesario habilitar el corrector en el dominio y en la página donde se va a ejecutar, así como especificar la propiedad de idioma para el dominio.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para ejecutar el corrector ortográfico.  
  
##  <a name="enable-the-speller"></a><a name="Enable"></a> Habilitar el corrector ortográfico  
  
1.  Para habilitar el corrector ortográfico en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], abra la base de conocimiento en la actividad **Administración de dominios** , seleccione el dominio que desee y haga clic en **Habilitar corrector ortográfico** en la página **Propiedades del dominio** . En **Idioma**, seleccione el idioma que se va a utilizar con el corrector ortográfico.  
  
2.  Si se habilita el corrector ortográfico en las propiedades de dominio, también lo hará en la páginas **Administrar valores del dominio** , **Valores del dominio** , **Relaciones basadas en términos** y **Administrar y ver resultados** . Para deshabilitar el corrector ortográfico en estas páginas, haga clic en el icono **Habilitar o deshabilitar el corrector ortográfico** . Haga clic en el icono en cada una de estas páginas para cambiar el estado del corrector ortográfico en ella. Del mismo modo, si la propiedad **Habilitar corrector ortográfico** del dominio está deshabilitada, haga clic en el icono **Habilitar o deshabilitar el corrector ortográfico** para habilitar el corrector ortográfico en la página. Si abandona la página y vuelve a ella a continuación, el estado del botón estará determinado nuevamente por la propiedad de dominio **Habilitar corrector ortográfico** .  
  
##  <a name="use-the-speller"></a><a name="Use"></a> Utilizar el corrector ortográfico  
  
1.  Desplácese a una de las páginas siguientes:  
  
    -   La página **Administrar valores del dominio** de la actividad **Detección de conocimiento**  
  
    -   La página **Valores del dominio** o **Relaciones basadas en términos** de la actividad **Administración de dominios**  
  
    -   La página **Administrar y ver resultados** de la actividad **Limpieza**  
  
2.  Muestre los valores apropiados en la tabla **Valor** aplicando un filtro o realizando una búsqueda.  
  
3.  Examine las filas de la tabla **Valor** para determinar si hay algún valor que aparezca subrayado con una línea ondulada de color rojo en las columnas **Valor** o **Corregir a** .  
  
4.  Haga clic con el botón secundario en un valor que esté marcado con un subrayado rojo. Haga clic en uno de los valores de reemplazo enumerados si es preferible al valor original.  
  
5.  Si ninguno de los valores mostrados es preferible al original, y hay un botón **Más sugerencias** que indica la existencia de valores adicionales, haga clic en él. Si uno de los valores adicionales es preferible al original, haga clic en él.  
  
6.  Si desea agregar el valor al diccionario, haga clic en **Agregar al diccionario**. El carácter de subrayado rojo desaparecerá del valor.  
  
##  <a name="follow-up-after-using-the-speller"></a><a name="FollowUp"></a> Seguimiento: después de utilizar el corrector ortográfico  
 Una vez ejecutado el corrector ortográfico, complete la actividad en la que se encuentra el dominio para usar las correcciones sugeridas por dicho corrector. Si se encuentra en la actividad Detección de conocimiento, Administración de dominios o Directiva de coincidencia, publique la base de conocimiento para que los resultados del análisis del corrector ortográfico estén disponibles para su uso en ella. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="how-the-speller-works"></a><a name="How"></a> Cómo funciona el corrector ortográfico  
 El corrector ortográfico de DQS marca los posibles errores de valor de cadena con un carácter de subrayado rojo que se muestra en todo el valor. Por ejemplo, si "New York" está escrito incorrectamente como "Neu York", el corrector ortográfico mostrará un subrayado de color rojo debajo de "Neu York", no solo de "Neu". Si hace clic con el botón secundario en el valor, verá las correcciones sugeridas para el valor completo. También puede hacer clic en **Más sugerencias** si hay más de cinco sugerencias. Puede elegir una de las sugerencias o agregar un valor al diccionario (en el nivel de cuenta de usuario) que se mostrará para el valor original. Los valores agregados al diccionario se aplican a todos los dominios. La corrección se realizará en el dominio únicamente si se designa explícitamente una sugerencia. Al seleccionar una sugerencia en el menú contextual del corrector ortográfico, el tipo de valor pasará a ser (o permanecerá como) erróneo. La sugerencia seleccionada se agregará a la columna de corrección. Tenga en cuenta que el **Tipo** de un valor puede ser **Correcto** y aun así estar marcado como posible error por el corrector ortográfico.  
  
 DQS proporcionará las sugerencias para los valores de las columnas **Valor** y **Corregir a** de la tabla **Valor** . Al seleccionar una sugerencia en la columna **Valor** , el tipo de valor se establece en **Error**y la sugerencia se copia en la columna **Corregir a** , como si se hubiera insertado manualmente. Si hubiera una corrección existente, se convertiría en una sugerencia. En la página **Administrar y ver resultados** de la actividad **Limpieza** , al seleccionar una sugerencia en la columna **Corregir a** , DQS reemplazará el valor seleccionado actualmente por la selección, y dicho valor se convertirá en una sugerencia. En la página **Administrar y ver resultados** de la actividad **Limpieza** , no se realizan sugerencias en el nivel de registro (la cuadrícula inferior).  
  
  
