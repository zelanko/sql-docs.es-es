---
title: Crear una regla entre dominios
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.testcdrule.f1
- sql13.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
author: swinarko
ms.author: sawinark
ms.openlocfilehash: b42733965fc41662ba81514da59460a0d02d5ac8
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812206"
---
# <a name="create-a-cross-domain-rule"></a>Crear una regla entre dominios

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En este tema se describe cómo crear una regla entre dominios para un dominio compuesto en una base de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Una regla entre dominios comprueba la relación entre los valores de los dominios individuales incluidos en un dominio compuesto. Una regla entre dominios debe cumplirse en todo el dominio compuesto para que los valores de dominio se consideren precisos y compatibles con los requisitos empresariales. Las reglas entre dominios se utilizan para validar, corregir y normalizar valores de dominio.  
  
 La cláusula If de una regla entre dominios se define para uno de los dominios individuales del dominio compuesto y la cláusula Then para otro distinto. Se debe definir cada una de las cláusulas para un dominio individual distinto. Una regla entre dominios debe estar relacionada con varios dominios individuales; no es posible definir una regla de dominio simple (solo para un dominio individual) para un dominio compuesto. Para ello, deberá definir una regla de dominio para un dominio individual. Cada una de las cláusulas If y Then puede contener una o varias condiciones.  
  
 Una regla entre dominios que tenga condiciones definitivas aplicará la lógica de la regla a los sinónimos del valor en las condiciones, así como a los propios valores. Las condiciones definitivas para las cláusulas If y Then son El valor es igual a, El valor no es igual a, El valor está en o El valor no está en. Por ejemplo, imagine que dispone de la siguiente regla entre dominios para un dominio compuesto: "Para "City", si el valor es igual a "Los Angeles", entonces para "State", el valor es igual a "CA"". Si "Los Angeles" y "LA" son sinónimos, esta regla dará un resultado correcto para "Los Angeles CA" y "LA CA", y un error para "Los Angeles WA" y "LA WA".  
  
 Además de permitirle conocer la validez de una regla entre dominios, la cláusula *Then* definitiva **El valor es igual a**de una regla entre dominios también corrige los datos durante la actividad de limpieza de datos. Para obtener más información, vea [Data Correction using Definitive Cross-Domain Rules](../data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) en [Cleanse Data in a Composite Domain](../data-quality-services/cleanse-data-in-a-composite-domain.md).  
  
 Las reglas entre dominios se tienen en consideración una vez aplicadas todas las reglas sencillas que afectan únicamente a un dominio individual. La regla entre dominios solo se aplica si un valor pasa las reglas de dominio individual (si estas existen). El dominio compuesto y los dominios individuales en los que se ejecuta una regla deben haberse definido con anterioridad a la ejecución de la regla.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Para poder crear una regla entre dominios, debe haber creado y abierto un dominio compuesto.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para crear una regla entre dominios.  
  
##  <a name="create-cross-domain-rules"></a><a name="Create"></a> Crear reglas entre dominios  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra o cree una base de conocimiento. Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Abrir** o en **Crear**. Para obtener más información, consulte [Crear una base de conocimiento](../data-quality-services/create-a-knowledge-base.md) o [Abrir una base de conocimiento](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La administración de dominios se realiza en una página del cliente de Data Quality Services que contiene cinco pestañas para distintas operaciones de administración de dominios. No se trata de un proceso controlado mediante asistentes; cada una de las operaciones de administración se puede realizar por separado.  
  
3.  En la **Lista de dominios** de la página **Administración de dominios** , seleccione el dominio compuesto para el que desea crear una regla de dominio, o cree un nuevo dominio compuesto. Si necesita crear un nuevo dominio, vea [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
4.  Haga clic en la pestaña **Reglas de CD** .  
  
5.  Haga clic en **Agregar una nueva regla de dominio**y escriba un nombre y una descripción para la regla.  
  
6.  Active la casilla **Activa** para especificar que la regla se debe ejecutar (el valor predeterminado) o anule dicha selección para impedir su ejecución.  
  
7.  Cree la cláusula If de la manera siguiente:  
  
    1.  En la lista de dominios del panel de cláusulas If, seleccione uno de los dominios individuales incluidos en el dominio compuesto como el sujeto de la cláusula If. Puede seleccionar cualquier dominio individual del dominio compuesto.  
  
    2.  Seleccione una condición en la lista desplegable para la primera condición de la cláusula.  
  
    3.  Si la condición requiere un valor, escríbalo en el cuadro de texto asociado con la condición.  
  
    4.  Si la cláusula If requiere otra condición, haga clic en **Agrega una nueva condición a la cláusula seleccionada**. Seleccione el operador, seleccione una condición y escriba un valor para esta, si es necesario.  
  
    5.  Para cambiar el orden de las condiciones, seleccione una de ellas haciendo clic a su izquierda y, a continuación, haga clic en la flecha arriba o en la flecha abajo.  
  
    6.  Para ocultar las condiciones, haga clic en el signo menos situado a la izquierda del nombre del dominio. Haga clic en el signo más para mostrar las condiciones.  
  
8.  Cree la cláusula Then seleccionando un dominio individual, distinto del sujeto de la cláusula If, en la lista de dominios que aparece en el panel de cláusulas Then. A continuación, genere la cláusula Then siguiendo los mismos pasos utilizados para la cláusula If.  
  
9. Continúe con el procedimiento de prueba descrito a continuación.  
  
##  <a name="test-cross-domain-rules"></a><a name="Test"></a> Probar reglas entre dominios  
  
1.  Pruebe la regla entre dominios de la manera siguiente:  
  
    1.  Haga clic en el icono **Ejecutar la regla de dominio seleccionada en los datos de prueba** en la esquina superior derecha del panel de dominios compuestos.  
  
    2.  En el cuadro de diálogo **Probar regla de dominio** , haga clic en el icono **Agrega un nuevo término de prueba para la regla de dominio** .  
  
    3.  Escriba los valores de prueba para los dominios individuales asociados con las cláusulas If y Then. Los valores de prueba escritos en la cláusula If deben cumplir las condiciones de dicha cláusula; en caso contrario, se incluirá un signo de interrogación en la columna **Validez** que indicará que la regla entre dominios no se aplica a los datos de prueba.  
  
    4.  Haga clic de nuevo en el icono **Agrega un nuevo término de prueba para la regla de dominio** para agregar otro conjunto de valores de prueba.  
  
    5.  Haga clic en el icono **probar la regla de dominio en todos los términos** . Si un conjunto de valores de prueba es válido, DQS incluirá una marca de comprobación en la columna **Validez** de la fila. Si el conjunto de valores de prueba no es válido, DQS incluirá un triángulo con un signo de exclamación en la columna Validez de la fila.  
  
    6.  Una vez finalizada la prueba, haga clic en **Cerrar** en el cuadro de diálogo **Probar regla de dominio compuesto** .  
  
2.  Cuando haya terminado de definir las reglas entre dominios, haga clic en **Finalizar** para finalizar la actividad de administración de dominios, tal como se describe en [End the Domain Management Activity](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="follow-up-after-creating-a-cross-domain-rule"></a><a name="FollowUp"></a> Seguimiento: después de crear una regla entre dominios  
 Una vez creada una regla entre dominios, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
  
