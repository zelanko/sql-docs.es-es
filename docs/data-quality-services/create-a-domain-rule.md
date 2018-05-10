---
title: Crear una regla de dominio | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.testdomainrule.f1
- sql13.dqs.dm.rules.f1
ms.assetid: 339fa10d-e22c-4468-b366-080c33f1a23f
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3b1103a3528674c8541aa04569e0d63a17ddcefc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-domain-rule"></a>Cree una regla de dominio

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo crear una regla de dominio en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Una regla de dominio es una condición que se utiliza para validar, corregir y normalizar valores de dominio. Una regla de dominio debe cumplirse en todo el dominio para que los valores de dominio se consideren precisos y compatibles con los requisitos empresariales. Las reglas de dominio pueden incluir reglas de validación que se utilizan para validar valores de dominio, pero no para corregir datos en los proyectos de calidad de datos. Las reglas también incluyen reglas de normalización que se aplican a los datos válidos y se utilizan en la corrección de datos.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para crear una regla de dominio, es necesario tener una base de conocimiento y un dominio abiertos en la actividad Administración de dominios.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para crear una regla de dominio.  
  
##  <a name="Build"></a> Crear reglas de dominio  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra o cree una base de conocimiento. Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Abrir** o en **Crear**. Para obtener más información, consulte [Crear una base de conocimiento](../data-quality-services/create-a-knowledge-base.md) o [Abrir una base de conocimiento](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La administración de dominios se realiza en una página del cliente de Data Quality Services que contiene cinco pestañas para distintas operaciones de administración de dominios. No se trata de un proceso controlado mediante asistentes; cada una de las operaciones de administración se puede realizar por separado.  
  
3.  En la **Lista de dominios** de la página **Administración de dominios** , seleccione el dominio para el que desea crear una regla de dominio, o cree uno nuevo. Si necesita crear un nuevo dominio, vea [Crear un dominio](../data-quality-services/create-a-domain.md).  
  
4.  Haga clic en la pestaña **Reglas de dominio** .  
  
5.  Haga clic en **Agregar una nueva regla de dominio**y, a continuación, escriba un nombre que sea único en la base de conocimiento y una descripción para la regla.  
  
6.  Active la casilla **Activa** para especificar que la regla se debe ejecutar (el valor predeterminado) o anule dicha selección para impedir su ejecución.  
  
7.  En el panel **Generar una regla** , seleccione una condición en la lista desplegable del cuadro de cláusulas de la regla.  
  
8.  Si la condición requiere un valor, escríbalo en el cuadro de texto asociado.  
  
9. Si necesita agregar otra cláusula, haga clic en **Agrega una nueva condición a la cláusula seleccionada** .  
  
10. Seleccione **AND** u **OR** como operador.  
  
11. Seleccione una condición en la lista desplegable y escriba un valor para el operando, si fuera necesario.  
  
12. Para cambiar el orden en el que aparecen las cláusulas en la lista, seleccione una cláusula y haga clic en la flecha arriba o abajo. Esto también cambiará el orden en el que se ejecutan, lo que puede afectar a los resultados.  
  
13. Agregue más cláusulas si es necesario. Si necesita eliminar una cláusula, selecciónela y haga clic en **Elimina la cláusula seleccionada**.  
  
14. Repita los pasos anteriores para agregar nuevas reglas si es necesario.  
  
15. Si desea ver el efecto que tendría una regla de validación en los valores si se implementa, haga clic en el icono **Analizar el impacto de la regla de dominio en los valores de dominio** .  
  
16. Continúe con el procedimiento de prueba descrito a continuación.  
  
##  <a name="Test"></a> Probar reglas de dominio  
  
1.  Seleccione una regla y haga clic en el icono **Ejecutar la regla de dominio seleccionada en los datos de prueba** .  
  
2.  En el cuadro de diálogo Probar regla de dominio, haga clic en el icono **Agrega un nuevo término de prueba para la regla de dominio** . Escriba el valor que desea probar. Escriba otros valores si es necesario. Seleccione un valor y haga clic en el icono **Quitar el término de prueba seleccionado** si fuera necesario.  
  
3.  Haga clic en el icono **Probar la regla de dominio en todos los términos** .  
  
4.  Compruebe la validez de cada uno de los términos. Una marca de comprobación significa “correcto”, una cruz significa “error” y un triángulo significa “no válido”.  
  
5.  Haga clic en **Cerrar** cuando haya terminado con el cuadro de diálogo de prueba.  
  
6.  Repita este procedimiento para otras reglas si es necesario.  
  
7.  Continúe con el procedimiento de aplicación descrito a continuación.  
  
##  <a name="Apply"></a> Aplicar reglas de dominio  
  
1.  Haga clic en **Aplicar todas las reglas** para aplicar las reglas a los valores del dominio. Al hacer clic en **Aplicar todas las reglas**, aparecerá un cuadro emergente que indicará cuántos valores en determinados estados se verán afectados por la regla. Haga clic en **Sí** si desea aplicar la regla, o en **No** en caso contrario. Si hace clic en **Sí**, haga clic en **Aceptar** para cerrar el cuadro emergente de resultados.  
  
    > [!NOTE]  
    >  Cuando cree o cambie una regla, no es necesario que guarde los cambios. Sin embargo, debe aplicar la regla para que los cambios surtan efecto.  
  
2.  Haga clic en **Descartar todos los cambios** para quitar los cambios realizados en las reglas de dominio y volver a las reglas aplicadas previamente, con lo que los cambios efectuados después de la última aplicación de las reglas no se aplicarán. La validez de cada uno de los valores del dominio se actualizará de acuerdo con las reglas previamente aplicadas, no con los cambios descartados.  
  
3.  Haga clic en **Finalizar** para finalizar la actividad de administración de dominios, tal como se describe en [Finalizar la actividad Administración de dominios](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear una regla de dominio  
 Una vez creada una regla de dominio, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Conditions"></a> Condiciones de las reglas de dominio  
 En la tabla siguiente se describen las condiciones que se pueden aplicar en la regla de dominio, y proporciona ejemplos que muestran cómo se pueden aplicar las condiciones.  
  
 Cuando se aplica una regla de dominio y un valor de dominio no la cumple, este valor se designa como no válido. Un valor designado como No válido se cambiará a Correcto si se elimina la regla que le llevó a ese estado, o se modifica dicha regla para que el valor la cumpla. Si ha designado un valor como No válido manualmente (en la pestaña Valores del dominio de la actividad Administración de dominios), y se elimina, desactiva o modifica una regla que el valor no cumple, el valor seguirá designándose como No válido, de acuerdo con la designación manual.  
  
 Una regla de dominio que tenga una condición definitiva aplicará la lógica de la regla a los sinónimos del valor en las condiciones, así como a los propios valores. Las condiciones definitivas son El valor es igual al, El valor no es igual a, El valor está en o El valor no está en. Por ejemplo, imagine que tiene la regla de dominio siguiente: “For ‘City’, El valor es igual a ‘Los Angeles’”. Si “Los Ángeles” y “LA” son sinónimos, ambos serán correctos. Por otro lado, si la regla no contenía una condición definitiva, por ejemplo “For City, El valor termina por “s”, entonces “Los Angeles” sería correcto, pero no así su sinónimo “LA”.  
  
 Puede elegir entre distintas alternativas al crear una regla de dominio. Por ejemplo, para validar si los valores comienzan por la letra A, B o C, podría crear una regla simple con una condición compleja (como una expresión regular con caracteres de barra vertical), o una regla compleja que contenga varias condiciones simples. Un ejemplo de la primera regla sería “El valor coincide con la expresión regular (^A|^B|^C)”. Un ejemplo de la segunda regla sería “’El valor comienza por A’ OR ‘El valor comienza por B’ OR ‘El valor comienza por C’”.  
  
|Condición|Description|Ejemplo|  
|---------------|-----------------|-------------|  
|La longitud es igual a|Solo serán válidos los valores que constan del número de caracteres designado por el operando.|Operando de ejemplo: 3<br /><br /> Valor válido: BB1<br /><br /> Valor no válido: AA|  
|La longitud es mayor o igual que|Solo serán válidos los valores que constan al menos del número de caracteres designado por el operando.|Operando de ejemplo: 3<br /><br /> Valores válidos: BB1, BBAA<br /><br /> Valor no válido: AA|  
|La longitud es menor o igual que|Solo serán válidos los valores que constan como máximo del número de caracteres designado por el operando.|Operando de ejemplo: 3<br /><br /> Valores válidos: BB1, AA<br /><br /> Valor no válido: BBAA|  
|El valor es igual a|Solo serán válidos los valores que son idénticos al operando.|Operando de ejemplo: BB1<br /><br /> Valor válido: BB1<br /><br /> Valores no válidos: BB, BB1#|  
|El valor no es igual a|Solo serán válidos los valores que no son idénticos al operando.|Operando de ejemplo: BB1<br /><br /> Valores válidos: BB, BB1#<br /><br /> Valor no válido: BB1|  
|El valor contiene|Solo serán válidos aquellos valores en los que todos sus caracteres estén incluidos en el operando, sin importar la posición que ocupan.|Operando de ejemplo: A1<br /><br /> Valores válidos: A1, AA1<br /><br /> Valores no válidos: 1A, AA|  
|El valor no contiene|Solo serán válidos los valores en los que no esté incluido el operando.|Operando de ejemplo: A1<br /><br /> Valores válidos: 1A, AA<br /><br /> Valores no válidos: A1, AA1|  
|El valor comienza por|Solo serán válidos los valores que empiezan por los caracteres del operando.|Operando de ejemplo: AA<br /><br /> Valor válido: AA1<br /><br /> Valor no válido: 1AAB|  
|El valor termina por|Solo serán válidos los valores que terminan por los caracteres del operando.|Operando de ejemplo: AA<br /><br /> Valores válidos: 1AA<br /><br /> Valor no válido: 1AAB|  
|El valor es numérico|Solo serán válidos los valores con un tipo de datos numérico de SQL Server. Esto incluye los tipos int, decimal, float, etc.|Operando de ejemplo: N/D<br /><br /> Valores válidos: -1, 25 y 345,1234.<br /><br /> Valores no válidos: 2b, bcdef|  
|El valor es fecha u hora|Solo serán válidos los valores con un tipo de datos de fecha y hora de SQL Server. Esto incluye los tipos datetime, time, date, etc.|Operando de ejemplo: N/D<br /><br /> Valores válidos: 1916-06-04; 1916-06-04 18:24:24; 21 de marzo de 2001; 5/18/2011; 18:24:24<br /><br /> Valores no válidos: marzo 213, 2006|  
|El valor está en|Solo serán válidos los valores que están en el conjunto del operando.<br /><br /> Para especificar los valores del conjunto, haga clic en el cuadro de texto del operando, escriba el primer valor, presione Entrar, escriba el segundo valor, repita este procedimiento con tantos valores como desee incluir en el conjunto y, a continuación, haga clic de nuevo en el cuadro de texto del operando. DQS insertará una coma entre los valores del conjunto. Si especifica una única cadena con comas y sin un retorno de carro (por ejemplo, “A1, B1"), DQS considerará dicha cadena como un valor único del conjunto.|Operando de ejemplo: [A1, B1]<br /><br /> Valores válidos: A1, B1<br /><br /> Valores no válidos: AA, 11|  
|El valor no está en|Solo serán válidos los valores que no están en el conjunto del operando.|Operando de ejemplo: [A1, B1]<br /><br /> Valores válidos: AA, 11<br /><br /> Valores no válidos: A1, B1|  
|El valor coincide con el modelo|Solo serán válidos los valores que coincidan con el modelo de caracteres, dígitos o caracteres especiales del operando.<br /><br /> Se puede usar cualquier letra (A…Z) como patrón para cualquier letra; no se distinguen mayúsculas de minúsculas. Se puede usar cualquier dígito (0…9) como patrón para cualquier dígito. Se puede usar cualquier carácter especial, excepto una letra o un dígito, como patrón de sí mismo. Los corchetes, [], definen una coincidencia opcional.|Operando de ejemplo: AA:000 (un patrón de *cualesquiera* dos caracteres seguidos de un signo de dos puntos (:), que a su vez va seguido de *cualesquiera* tres dígitos.<br /><br /> Valores válidos: AB:012, df:257<br /><br /> Valores no válidos: abc:123, FJ-369<br /><br /> Para obtener más información sobre las reglas de patrón en DQS y ejemplos, vea [Coincidencias de patrón en reglas de dominio de DQS](http://blogs.msdn.com/b/dqs/archive/2012/10/08/pattern-matching-in-dqs-domain-rules.aspx).|  
|El valor no coincide con el modelo|Solo serán válidos los valores que no coincidan con el modelo de caracteres, dígitos o caracteres especiales del operando.|Operando de ejemplo: A1 (el valor no debe coincidir con un patrón de *cualquier* carácter seguido de *cualquier* dígito).<br /><br /> Valores válidos: AB1, A, A:5<br /><br /> Valores no válidos: B7, c9|  
|El valor contiene el modelo|Solo serán válidos los valores que contengan el modelo de caracteres, dígitos o caracteres especiales del operando.|Operando de ejemplo: AA-12 (el valor contiene un modelo de *cualesquiera* dos caracteres seguidos de un guion (-), que a su vez va seguido de *cualesquiera* dos dígitos).<br /><br /> Valores válidos: AAA-01, ab-975<br /><br /> Valores no válidos: A7, AA-6, C-45, aa;98|  
|El valor no contiene el modelo|Solo serán válidos los valores que no contengan el modelo de caracteres del operando.|Operando de ejemplo: AB-12 (el valor no debe contener un modelo de *cualesquiera* dos caracteres seguidos de un guion (-), que a su vez va seguido de *cualesquiera* dos dígitos).<br /><br /> Valores válidos: A7, AA-6, C-45, aa;98<br /><br /> Valores no válidos: AAA-01, ab-975|  
|El valor coincide con la expresión regular|Solo se considerarán válidos los valores que coincidan con la expresión regular del operando.<br /><br /> No incluya los delimitadores “^” ni “$” en la expresión regular, ya que DQS los agrega automáticamente a las cláusulas que contienen esta condición. (De forma alternativa, incluya entre paréntesis la expresión regular que contenga dichos delimitadores). Para obtener más información acerca de las expresiones regulares, vea [Elementos del lenguaje de expresiones regulares](http://go.microsoft.com/fwlink/?LinkId=225561).|Operando de ejemplo: [1-5] + (cada carácter debe ser un dígito numérico comprendido entre 1 y 5, apareciendo al menos una vez)<br /><br /> Valores válidos: 123, 12345, 14352<br /><br /> Valores no válidos: 456, ABC|  
|El valor no coincide con una expresión regular|Solo se considerarán válidos los valores que no coincidan con la expresión regular del operando.|Operando de ejemplo: [1-5] + (la cadena no debe esta formada únicamente por dígitos numéricos comprendidos entre 1 y 5)<br /><br /> Valores válidos: 456, ABC<br /><br /> Valores no válidos: 123, 123456, 14352|  
  
  
