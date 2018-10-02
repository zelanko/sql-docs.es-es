---
title: Crear un dominio compuesto | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.createcd.f1
- sql13.dqs.dm.cdproperties.f1
ms.assetid: c7f0bd84-a02e-4a81-885d-985e6415c499
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4efd1769b95a43b6718eaa635273458bc241f282
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776618"
---
# <a name="create-a-composite-domain"></a>Crear un dominio compuesto

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo crear un dominio compuesto en una base de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Un dominio compuesto consta de uno o varios dominios individuales que se aplican a un único campo de datos. Para más información sobre los dominios compuestos, vea [Administrar un dominio compuesto](../data-quality-services/managing-a-composite-domain.md).  
  
 Hay dos maneras de crear un nuevo dominio compuesto. La primera es durante el paso de asignación de la actividad de detección de conocimiento, cuando se analiza una muestra de los datos para agregar conocimiento a una base de conocimiento nueva o a una ya existente. La segunda es durante la actividad de administración de dominios, cuando se crea un nuevo dominio en lugar de modificar uno ya existente. Para crear un dominio compuesto, debe haber creado al menos dos dominios individuales para agregarlos al dominio compuesto. Cuando se crea un nuevo dominio compuesto, solo están disponibles los dominios individuales que ya se han creado y que no se han agregado a un dominio compuesto existente. Un dominio individual no se puede agregar a más de un dominio compuesto, y un dominio compuesto no se puede agregar a otro dominio compuesto.  
  
 Después de crear un dominio compuesto, puede cambiar las propiedades del mismo, adjuntar un servicio de datos de referencia al dominio, crear reglas entre dominios o crear relaciones de valor. Para ello, seleccione el dominio compuesto en la lista **Dominio** de la página **Administración de dominios** y seleccione la pestaña adecuada.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para crear un dominio compuesto, debe haber creado y abierto una base de conocimiento, y debe haber creado al menos dos dominios individuales para agregarlos al dominio compuesto.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para crear un dominio compuesto.  
  
##  <a name="ParsingKnowledgeDiscoveryActivity"></a> Crear un dominio compuesto en la actividad Detección de conocimiento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Abrir base de conocimiento** y seleccione una base de conocimiento, o haga clic en **Nueva base de conocimiento** y especifique las propiedades para la nueva base de conocimiento.  
  
3.  Seleccione **Detección de conocimiento** como actividad y, a continuación, haga clic en **Crear** para crear la nueva base de conocimiento o en **Abrir** para abrir una ya existente.  
  
4.  En la página **Asignación** , especifique una conexión con el origen de datos. Para obtener más información, vea [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
5.  En la tabla **Asignaciones** , seleccione una columna de origen en la lista desplegable para la columna **Columna de origen** de una fila vacía. Asegúrese de que la columna de origen contiene el dominio compuesto formado por dos dominios individuales existentes. Si no existe un dominio individual correspondiente, haga clic en el icono **Crear un dominio** .  
  
6.  En la tabla **Asignaciones** , seleccione una columna de origen en la lista desplegable para la columna **Columna de origen** de una fila vacía. Asegúrese de que la columna de origen contiene elementos de dominio compuesto asociados a dos dominios individuales existentes. Si no existen los dominios individuales correspondientes, haga clic en el icono **Crear un dominio** para crearlos. Para más información, consulte [Crear un dominio](../data-quality-services/create-a-domain.md).  
  
7.  Haga clic en el icono **Crear un dominio compuesto** .  
  
##  <a name="DomainManagementActivity"></a> Crear un dominio compuesto en la actividad Administración de dominios  
  
1.  En la página de inicio del cliente de Data Quality Services, haga clic en **Abrir base de conocimiento** y, a continuación, seleccione una base de conocimiento, o haga clic en **Nueva base de conocimiento** y especifique las propiedades de la nueva base de conocimiento.  
  
2.  Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Crear** para crear la nueva base de conocimiento o en **Abrir** para abrir una ya existente.  
  
3.  Asegúrese de que existen dos o más dominios individuales que son necesarios para el dominio compuesto. En caso contrario, haga clic en el icono **Crear un dominio** y créelos. Para más información, consulte [Crear un dominio](../data-quality-services/create-a-domain.md).  
  
4.  En la página **Administración de dominios** , haga clic en el icono **Crear un dominio compuesto** situado sobre la lista de dominios.  
  
5.  Escriba un nombre que sea único en la base de conocimiento y una descripción hasta 256 caracteres.  
  
6.  En la **Lista de dominios**, seleccione los dominios que formarán parte del dominio compuesto y, a continuación, haga clic en la flecha derecha para moverlos a la tabla **Dominios del dominio compuesto** .  
  
7.  Haga clic en **Aceptar**.  
  
##  <a name="CompositeDomainProperties"></a> Establecer las propiedades de un dominio compuesto  
  
1.  En el cuadro de diálogo **Crear dominio compuesto** , escriba un nombre que sea único en la base de conocimiento y una descripción con una longitud máxima de 256 caracteres.  
  
2.  En la **Lista de dominios**, seleccione los dominios que formarán parte del dominio compuesto y, a continuación, haga clic en la flecha derecha para moverlos a la tabla **Dominios del dominio compuesto** . Esta lista contiene los dominios individuales disponibles para agregarlos al dominio compuesto que está creando. Solo están disponibles los dominios individuales que se han creado y que no se hayan agregado a un dominio compuesto existente. Un dominio individual no se puede agregar a más de un dominio compuesto de la knowledge base, y un dominio compuesto no se puede agregar a otro dominio compuesto.  
  
3.  Haga clic en **Avanzadas**.  
  
4.  En **Método de análisis**, seleccione una de las opciones siguientes:  
  
    -   **Datos de referencia**: analiza los valores del campo dependiendo del formato que Reference Data Service (RDS) haya dado a los datos de referencia. Data Quality Services enviará los valores del dominio compuesto a RDS, y RDS devuelve datos corregidos y analizados en función del dominio compuesto.  
  
    -   **En orden**: analiza los valores de los campos según el orden que tienen los dominios en el dominio compuesto. El primer valor se incluirá en el primer dominio, el segundo valor en el segundo dominio, y así sucesivamente.  
  
    -   **Delimitadores**: analiza los valores del campo según el delimitador seleccionado en los botones de opción que se muestran cuando se selecciona Delimitadores. Pueden ser **Carácter de tabulación**, **Punto y coma**, **Coma**, **Espacio**u **Otros**. Si selecciona **Otros**, escriba el valor que servirá como delimitador.  
  
5.  Si selecciona **Delimitadores** como método de análisis, también puede seleccionar **Usar el análisis de bases de conocimiento**. Para obtener más información, consulte [Knowledge-Based Parsing](#KnowledgeBaseParsing).  
  
6.  Haga clic en **Finalizar** para finalizar la actividad de administración de dominios, tal como se describe en [Finalizar la actividad Administración de dominios](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear un dominio compuesto  
 Una vez creado el dominio compuesto, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="KnowledgeBaseParsing"></a> Knowledge-Based Parsing  
 Data Quality Services permite analizar los datos en función del conocimiento, no solo en función de los delimitadores o el orden. El análisis basado en conocimiento se utiliza cuando los datos de origen complejos están asignados a un dominio compuesto y no se están utilizando los servicios de datos de referencia. Puede utilizar el análisis basado en conocimiento para analizar los datos del origen de datos en los dominios individuales correspondientes. Con el análisis basado en conocimiento, DQS primero intentará utilizar el conocimiento para analizar datos complejos en dominios individuales. Si es posible, identificará partes de la cadena como pertenecientes a uno o varios dominios, y analizará la cadena en sus distintos dominios. Por ejemplo, supongamos que tiene “John B. Doe” como valor complejo en un campo de nombre completo representado por un dominio compuesto denominado Nombre completo. Si DQS identifica “John” como en el dominio Nombre y “Doe” como en el dominio Apellidos, DQS agregará “B.” al dominio Segundo nombre según el conocimiento de los dominios.  
  
 Solo puede utilizar el análisis basado en conocimiento si también selecciona el análisis basado en delimitadores. El análisis basado en conocimiento no reemplaza al análisis basado en delimitadores, sino que lo mejora. DQS solo utilizará un delimitador para realizar el análisis si no existe ningún conocimiento para hacerlo. En algunos casos, DQS puede determinar parte del análisis mediante el análisis basado en conocimiento y después determinar otra parte del análisis mediante el análisis basado en delimitadores.  
  
 El análisis basado en conocimiento se puede utilizar cuando el dominio compuesto consta de dominios de cadena o cuando el dominio compuesto consta de una combinación de varios tipos de dominios (int, date, time, etc.). Si el origen de datos consta de varios tipos de datos, el análisis debe realizarse primero para los tipos de datos que no son de cadena y después, como se ha descrito anteriormente, basándose en el conocimiento del dominio para el resto de los datos.  
  
 Si, cuando se utiliza el análisis basado en conocimiento, los datos de origen contienen un número de valores inferior al número de dominios que hay en el dominio compuesto, DQS colocará un valor NULL en el dominio que falta. Cuando los datos de origen contienen un número de valores superior al número de dominios que hay en el dominio compuesto, DQS agregará los datos adicionales a una de las columnas. Si dos o más dominios incluyen los mismos valores, el origen de datos se analizará para el primer dominio coincidente.  
  
  
