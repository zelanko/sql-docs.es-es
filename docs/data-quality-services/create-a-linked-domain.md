---
title: Crear un dominio vinculado | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.linkeddomain.f1
ms.assetid: fd99d422-c53d-4d7c-9cdd-303c703683b6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 231c1111dbdb6a56419c25d5f467c2813156780a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022098"
---
# <a name="create-a-linked-domain"></a>Crear dominio vinculado

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo crear un dominio vinculado en una base de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Los dominios vinculados se crean a partir de otros dominios previamente existentes, y heredan todos los valores, reglas y propiedades de los dominios a los que están vinculados, con la excepción del nombre y la descripción. Es posible administrar un conjunto de dominios vinculados como si fuera un único dominio. Al vincular un dominio al otro, se crea un dominio que hereda su contenido de otro dominio.  
  
## <a name="scenarios"></a>Escenarios  
 Los dominios vinculados son especialmente útiles en los escenarios siguientes.  
  
### <a name="mapping-multiple-fields-to-domains-that-share-values-rules-and-properties"></a>Asignar varios campos a dominios que comparten valores, reglas y propiedades  
 No se pueden asignar dos campos al mismo dominio, pero es posible asignar un campo a un dominio y, a continuación, asignar un segundo campo a un dominio vinculado al primero. De esta forma, se asignan los campos a dos dominios diferentes que tienen el mismo contenido y las mismas propiedades (excepto el nombre y la descripción). Para obtener más información, consulte [Map two fields to linked domains](#Map).  
  
### <a name="controlling-data-flow-to-composite-domains"></a>Controlar el flujo de datos a los dominios compuestos  
 Los dominios vinculados le permiten controlar el flujo de datos entre los campos y los dominios compuestos. Gracias a ellos, es posible diferenciar cuándo los datos de un campo fluyen en un dominio compuesto, y cuándo los datos de otro campo muy similar no lo hacen. Para conseguirlo, es necesario especificar que, de los dos dominios vinculados, uno forma parte de un dominio compuesto y el otro no. Desde una perspectiva de dominio, los dominios vinculados son idénticos. Ambos contienen el mismo conocimiento. Sin embargo, desde una perspectiva de dominio compuesto, los dominios vinculados son diferentes. Uno de ellos participa en el dominio compuesto, pero el otro no.  
  
 Un ejemplo es un registro que contiene los campos siguientes: Nombre del cliente, Apellidos del cliente y Nombre del padre. Imagine que asigna el nombre del cliente y el nombre del padre a un dominio Nombre, y que incluye tanto este como el dominio Apellidos en el dominio compuesto Nombre completo. El problema es que el nombre del padre se agregará al dominio compuesto sin apellidos. Pero si vincula cada uno de los dos campos de nombre a un dominio y vincula ambos dominios, podrá agregar el dominio Nombre del cliente al dominio compuesto Nombre completo, y no agregar el campo Nombre del padre a ese dominio, con lo que evitará que el Nombre del padre se agregue al dominio compuesto.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para crear un dominio vinculado, es necesario tener una base de conocimiento y un dominio existente al que desea vincular.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para crear un dominio vinculado.  
  
##  <a name="Create"></a> Crear dominio vinculado  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra o cree una base de conocimiento. Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Abrir** o en **Crear**. Para obtener más información, consulte [Crear una base de conocimiento](../data-quality-services/create-a-knowledge-base.md) o [Abrir una base de conocimiento](../data-quality-services/open-a-knowledge-base.md).  
  
3.  En la **lista de dominios** de la página **Administración de dominios** , haga clic con el botón secundario en el dominio con el que desea vincular un nuevo dominio y, a continuación, haga clic en **Crear dominio vinculado**.  
  
    > [!NOTE]  
    >  No existe ningún icono específico para crear un dominio vinculado. Esta acción solo se podrá realizar mediante el comando del menú contextual.  
  
4.  En el cuadro de diálogo **Crear dominio** , escriba un nombre que sea único en la base de conocimiento y una descripción con una longitud máxima de 256 caracteres. Compruebe que el nombre del dominio vinculado es correcto.  
  
5.  Haga clic **Aceptar** para completar la creación del dominio vinculado.  
  
6.  Si fuera necesario, puede cambiar el nombre o la descripción del dominio vinculado en la pestaña Propiedades del dominio.  
  
7.  Haga clic en **Finalizar** para finalizar la actividad de administración de dominios, tal como se describe en [Finalizar la actividad Administración de dominios](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="Map"></a> Map two fields to linked domains  
  
1.  Abra una base de conocimiento en la actividad de detección de conocimiento, y asígnela a la base de datos y la tabla o la vista.  
  
2.  Asigne un campo a un dominio y, a continuación, intente asignar un segundo campo al mismo dominio.  
  
3.  En el cuadro emergente que indica que el dominio ya está en uso, haga clic en Sí para crear un dominio vinculado.  
  
4.  En el cuadro de diálogo Crear dominio, escriba un nombre de dominio y una descripción; a continuación, haga clic en Aceptar.  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear un dominio vinculado  
 Una vez creado el dominio vinculado, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Behavior"></a> Comportamiento de un dominio vinculado  
 Puede cambiar la configuración de un dominio vinculado de la manera siguiente:  
  
-   Puede cambiar el nombre y la descripción de un dominio vinculado.  
  
-   Para cambiar las propiedades de dominio **Tipo de datos**, **Usar valores iniciales**o **Dar formato a la salida para** , seleccione el dominio con el que ha establecido el vínculo y modifique la configuración de la pestaña **Propiedades del dominio** para dicho dominio. Esta configuración no se puede cambiar en las propiedades del dominio vinculado. Para más información, consulte [Crear un dominio](../data-quality-services/create-a-domain.md).  
  
-   La configuración de las pestañas **Datos de referencia**, **Reglas de dominio**, **Valores del dominio**y **Relaciones basadas en términos** de la página Administración de dominios se puede cambiar tanto para el dominio vinculado como para el dominio al que está vinculado, y los cambios los heredará el otro dominio.  
  
 Los dominios vinculados tienen las características siguientes:  
  
-   No es posible desvincular dos dominios. Para quitar el vínculo, elimine uno de los dominios vinculados.  
  
-   Al seleccionar un dominio vinculado en la lista de dominios de la página Administración de dominios, la cadena que identifica al dominio vinculado en el panel que contiene la tabla **Valor** incluye una indicación de que el dominio es un dominio vinculado.  
  
-   Si elimina un dominio con el que está vinculado otro dominio, se eliminarán ambos dominios. No obstante, puede eliminar un dominio vinculado, y el dominio al que está vinculado este no se eliminará.  
  
-   Un dominio vinculado no se puede vincular a un dominio que a su vez esté vinculado a otro.  
  
-   No se puede crear un dominio vinculado o un dominio compuesto vinculado a un dominio compuesto.  
  
-   Al hacer doble clic en un dominio vinculado en cualquiera de las pestañas de la administración de dominios, el dominio se abrirá para su edición indicando en la cadena de nombre que es un dominio vinculado.  
  
  
