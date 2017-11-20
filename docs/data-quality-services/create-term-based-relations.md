---
title: "Crear relaciones basadas en términos | Microsoft Docs"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.dm.kbtermsbased.f1
ms.assetid: 66db9277-d892-4dae-8a82-060fd3ba6949
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 93965e0267bb988b2b833701c9f193385220ff90
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="create-term-based-relations"></a>Crear relaciones basadas en términos
  En este tema se describe cómo crear relaciones basadas en términos para un dominio de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Una relación basada en términos (TBR) permite corregir términos que forman parte de los valores de un dominio. Permiten considerar como sinónimos idénticos varios valores que son idénticos salvo por la ortografía de una parte común. Por ejemplo, podría configurar una relación basada en términos que cambiara el término “Inc.” por “Incorporated”. El término “Inc.” se cambiará cada vez que aparezca en el dominio. Las instancias de “Contoso, Inc.” se cambiarán por “Contoso, Incorporated”, y ambos valores se considerarán sinónimos exactos.  
  
 Para utilizar relaciones basadas en términos, es necesario crear una lista de pares formados por un valor y una corrección, como “Inc.” e “Incorporated” o “Sénior” y “Sr.”. Una relación basada en términos permite cambiar un término en todo el dominio sin necesidad de establecer manualmente como sinónimo cada valor del dominio. Puede indicar que se corrija un valor aunque el proceso de detección de conocimiento no lo haya detectado previamente. Si la transformación de una relación basada en términos hace que dos valores sean idénticos, DQS creará entre ellos una relación de sinónimos (en la detección del conocimiento), una relación de corrección (en la corrección de datos) o una coincidencia exacta (en la coincidencia).  
  
 Tanto la transformación de relaciones basadas en términos como la transformación de símbolos (en la que los caracteres especiales se sustituyen por espacios o valores NULL) se realizan en una fase previa al procesamiento, antes de análisis final. Si se solicita el análisis inicial de un dominio compuesto, este se realizará antes de las dos transformaciones, ya que el análisis inicial de delimitadores requiere el uso de símbolos. Otras operaciones, como los cambios en las reglas y en los valores del dominio, se llevan a cabo después de las transformaciones. En la coincidencia, las relaciones basadas en los términos se aplican a los datos de origen antes de la actividad de coincidencia independientemente de si se ejecuta una limpieza.  
  
 **Administración de dominios y relaciones basadas en términos**  
  
 Cuando se aplica una relación basada en términos en la administración de dominios, DQS aplicará los cambios en los procesos de detección del conocimiento, limpieza o coincidencia; sin embargo, DQS no cambia el propio valor para adecuarse a la relación basada en términos. Es decir, si escribe y acepta una relación basada en términos en la pestaña **Relaciones basadas en términos** de la página **Administración de dominio** , el cambio no se llevará a cabo en la pestaña **Valores del dominio** de la misma página. Esto permite cambiar la TBR posteriormente.  
  
 **Relaciones basadas en términos y y limpieza de datos**  
  
 Cuando se aplica una relación basada en términos en un dominio y después se ejecuta el proceso de limpieza de datos, DQS aplica los cambios durante la limpieza pero no aplica los cambios a los términos de la base de conocimiento.  
  
-   Si un valor según es modificado por una relación basada en términos está en el dominio, pero no es un sinónimo, se mostrará en la columna **Corregir a** en la pestaña **Corregido** de la página de **Administrar y ver resultados** , con la razón establecida en Relación basada en términos.  
  
-   Si un valor según es modificado por una relación basada en términos no se encuentra en el dominio y DQS encuentra un valor coincidente, el valor se corregirá a y aparecerá en la pestaña Corregido o en la pestaña Sugerido, según el nivel de confianza. Si no se encuentra ninguna coincidencia, el valor aparecerá debajo de Nuevo con una corrección de TBR. Esto se hace porque, incluso si corrige el TBR, no significa que el valor es el correcto.  
  
-   Si un valor según es modificado por una relación basada en términos se encuentra en el dominio, pero el valor es Error/No vaĺido con una corrección existente, el valor aparecerá en la pestaña Corregido con su corrección y el motivo Valor de dominio.  
  
-   Si un valor según esmodificado por una relación basada en términos se encuentra en el dominio, pero el valor es Error/No válido sin ninguna corrección, el valor aparecerá en la pestaña No válido con el motivo Valor de dominio.  
  
 **Relaciones basadas en términos y detección del conocimiento**  
  
 Cuando se aplica una relación basada en términos se ejecuta después el proceso de detección del conocimiento, cualquier valor que se ajuste al TBR permanecerá tal cual y se identificará como valor correcto. Cualquier valor que un TBR vambie se importará como valor correcto y se identificará como sinónimo en un valor que se ajuste al TBR.  
  
 **Relaciones basadas en trérminos e importar valores de limpieza en un dominio**  
  
 Si importa el conocimiento de calidad de los datos recopilados durante el proces ode limpieza en un dominio, valor que cambie un TBR se importará como valor correcto.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para crear relaciones basadas en términos, debe tener un dominio abierto en la actividad Administración de dominios.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para crear relaciones basadas en términos.  
  
##  <a name="Create"></a> Crear relaciones basadas en términos  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra o cree una base de conocimiento. Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Abrir** o en **Crear**. Para obtener más información, consulte [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) o [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La administración de dominios se realiza en una página del cliente de Data Quality Services que contiene cinco pestañas para distintas operaciones de administración de dominios. No se trata de un proceso controlado mediante asistentes; cada una de las operaciones de administración se puede realizar por separado.  
  
3.  En la **Lista de dominios** de la página **Administración de dominios** , seleccione el dominio para el que desea crear una regla de dominio, o cree uno nuevo. Si necesita crear un nuevo dominio, vea [Create a Domain](../data-quality-services/create-a-domain.md).  
  
4.  Haga clic en la pestaña **Relaciones basadas en términos** .  
  
5.  Cree las relaciones basadas en términos de la siguiente manera:  
  
    1.  Haga clic en **Agregar nueva relación** para agregar una fila a la tabla de relaciones.  
  
    2.  En la columna **Valor** de la fila que ha agregado, escriba el término que desea cambiar cada vez que aparezca en un valor del dominio seleccionado.  
  
        > [!NOTE]  
        >  Si el término existe en el dominio como valor completo o como valor de corrección, obtendrá un error.  
  
    3.  En la columna **Corregir a** , escriba el término por el que desea cambiar el término de la columna **Valor** .  
  
    4.  Vuelva a hacer clic en **Agregar nueva relación** para agregar otra relación basada en términos.  
  
    5.  Haga clic en **Eliminar las relaciones seleccionadas** para eliminar de la tabla de relaciones una o varias filas seleccionadas. Si lo desea, puede seleccionar varias filas; para ello, presione la tecla Ctrl y haga clic en una fila que no esté seleccionada.  
  
    6.  Busque un valor en la tabla de relaciones; para ello, especifique uno o varios caracteres en el cuadro de texto **Buscar** . Se resaltarán las cadenas que coincidan con la especificada. Utilice las flechas arriba y abajo para desplazarse por las distintas instancias de la cadena en la tabla.  
  
    7.  **Corrector ortográfico**: si un valor de la columna **Valor** o **Corregir a** tiene un carácter de subrayado rojo ondulado, el corrector ortográfico está sugiriendo una corrección al valor. Haga clic con el botón secundario en el valor que tiene el carácter de subrayado y seleccione uno de los valores propuestos por el corrector ortográfico. O bien, puede hacer clic en **Agregar** en el menú contextual para seguir usando el valor original. Para obtener más información, consulte [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md) y [Set Domain Properties](../data-quality-services/set-domain-properties.md).  
  
        > [!NOTE]  
        >  Para utilizar el corrector ortográfico, puede habilitarlo en la página **Propiedades del dominio** o, si está deshabilitado en la página **Propiedades del dominio** , puede hacer clic en el icono **Habilitar o deshabilitar el corrector ortográfico** de la página **Relaciones basadas en términos** para habilitarlo en esta página.  
  
6.  Haga clic en **Aplicar cambios** para aplicar las relaciones basadas en el término al dominio.  
  
7.  Haga clic en **Finalizar** para finalizar la actividad de administración de dominios, tal como se describe en [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear las relaciones basadas en términos  
 Una vez creadas las relaciones basadas en términos, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
  

