---
title: Definir una relación varios a varios y las propiedades de relación de varios a varios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- many-to-many relationships [Analysis Services]
ms.assetid: edb5f61a-a581-467a-a367-134b7f9b849f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2c521e524e6e205989e2bff96928af4da9c24bb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091882"
---
# <a name="define-a-many-to-many-relationship-and-many-to-many-relationship-properties"></a>Definir una relación de varios a varios y las propiedades de las relaciones de varios a varios
  En este tema se explican las dimensiones varios a varios de Analysis Services, incluido cuándo usarlas y cómo crearlas.  
  
## <a name="introduction"></a>Introducción  
 Analysis Services admite dimensiones varios a varios, lo que permite realizar análisis más complejos que los que se pueden describir en un esquema de estrella clásico. En un esquema de estrella clásico, todas las dimensiones tienen una relación uno a varios con un tabla de hechos. Cada hecho se combina con un miembro de dimensión; un único miembro de dimensión está asociado a varios hechos.  
  
 La relación de varios a varios elimina esta restricción de modelado al permitir que un hecho (como el saldo de una cuenta) se asocie a varios miembros de la misma dimensión (el saldo de una cuenta conjunta se puede atribuir a dos o más propietarios de una cuenta conjunta).  
  
 Conceptualmente, una relación dimensional de varios a varios en Analysis Services es equivalente a las relaciones de varios a varios de un modelo relacional y admite los mismos tipos de escenarios. He aquí algunos ejemplos de relaciones de varios a varios:  
  
-   Los alumnos se inscriben en varios cursos; cada curso tiene varios alumnos.  
  
-   Los médicos tienen varios pacientes; los pacientes tienen varios médicos.  
  
-   Los clientes tienen varias cuentas bancarias; las cuentas bancarias pueden pertenecer a más de un cliente.  
  
-   En Adventure Works, varios clientes tienen varias razones para pedir un producto, y un motivo de venta puede estar asociado a varios pedidos.  
  
 Analíticamente, el problema que resuelve una relación de varios a varios es una representación exacta de un recuento o una suma con respecto a la relación dimensional (eliminando normalmente los dobles recuentos al realizar cálculos para un miembro de dimensión determinado). Es necesario ver un ejemplo para aclarar este concepto. Imagine un producto o un servicio que pertenece a más de una categoría. Si estuviera contando el número de servicios por categoría, querría que un servicio que pertenezca a ambas categorías se incluyera en todas las categorías. Al mismo tiempo, no querría exagerar el número de servicios que proporciona. Al especificar la relación dimensional de varios a varios, es más probable que obtenga los resultados correctos al consultar por categoría o por servicio. Sin embargo, siempre es necesario realizar pruebas exhaustivas para asegurarse de que este es el caso.  
  
 Estructuralmente, la creación de una relación dimensional de varios a varios es similar a la creación de una relación de varios a varios en un modelo de datos relacionales. Mientras que un modelo relacional emplea una *tabla de unión* para almacenar las asociaciones de filas, un modelo multidimensional utiliza un *grupo de medida intermedio*. El grupo de medida intermedio es el término que usamos para referirnos a una tabla que asigna miembros de distintas dimensiones.  
  
 Visualmente, una relación dimensional de varios a varios no se indica en un diagrama de cubo. En su lugar, usa la pestaña Uso de dimensiones para identificar rápidamente cualquier relación de varios a varios de un modelo. Una relación de varios a varios se indica mediante el icono siguiente.  
  
 ![Icono de varios a varios en el uso de dimensiones](../media/ssas-m2m-icondimusage.png "-to-many icono en el uso de dimensiones")  
  
 Haga clic en el botón para abrir el cuadro de diálogo Definir relación con el fin de comprobar que el tipo de relación es varios a varios y ver qué grupo de medida intermedio se emplea en la relación.  
  
 ![Botón de la relación de definir en el uso de dimensiones](../media/ssas-m2m-btndimusage.png "botón Definir relación en el uso de dimensiones")  
  
 En secciones posteriores aprenderá a configurar una dimensión varios a varios y probar los comportamientos del modelo. Si prefiere ver información adicional o seguir algún tutorial primero, vea **Más información** al final de este artículo.  
  
## <a name="create-a-many-to-many-dimension"></a>Crear una dimensión varios a varios  
 Una relación de varios a varios sencilla incluye dos dimensiones que tienen una cardinalidad varios a varios, un grupo de medida intermedio para almacenar asociaciones de miembros y un grupo de medida de hechos que contiene datos que se pueden medir, como una suma de ventas totales o el saldo de una cuenta bancaria.  
  
 Las dimensiones de una relación de varios a varios pueden tener tablas correspondientes en la vista del origen de datos, donde cada dimensión del modelo se basa en una tabla existente en un origen de datos. Por el contrario, las dimensiones del modelo pueden derivar de menos tablas físicas o de tablas físicas diferentes de la vista del origen de datos. Usando Razones de venta y Pedidos de venta como ejemplo, el cubo de ejemplo de Adventure Works muestra una relación de varios a varios que usa dimensiones que existen como estructuras de datos solo del modelo, sin homólogos físicos en la vista del origen de datos. La dimensión Pedidos de venta se basa en una tabla de hechos, no en una tabla de dimensiones, del origen de datos subyacente.  
  
 En el procedimiento siguiente se da por supuesto que ya sabe qué entidades participan en la relación de varios a varios. Vea **Más información** si desea más información al respecto.  
  
 Con el fin de ilustrar los pasos necesarios para crear una relación de varios a varios, en este procedimiento se vuelve a crear una de las relaciones de varios a varios del cubo de ejemplo de Adventure Works. Si tiene el origen de datos (es decir, el almacenamiento de datos de ejemplo Adventure Works) instalado en una instancia de un motor de base de datos relacional, puede seguir estos pasos.  
  
#### <a name="step-1-verify-dsv-relationships"></a>Paso 1: comprobar las relaciones de la vista del origen de datos  
  
1.  En SQL Server Data Tools, en un proyecto multidimensional, cree un origen de datos en el almacenamiento de datos relacional Adventure Works DW 2012, hospedado en una instancia de Motor de base de datos de SQL Server.  
  
2.  Cree una vista del origen de datos con las siguientes tablas existentes:  
  
    -   FactInternetSales  
  
    -   FactInternetSalesReason  
  
    -   DimSalesReason  
  
3.  Compruebe que todas las tablas que piensa usar en las relaciones de varios a varios están relacionadas en la vista del origen de datos mediante relaciones de clave principal. Esto es obligatorio para poder establecer un vínculo al grupo de medida intermedio en un paso posterior.  
  
    > [!NOTE]  
    >  Si el origen de datos subyacente no proporciona relaciones de clave principal y externa, puede crear las relaciones manualmente en la vista del origen de datos. Para más información, vea [Definir relaciones lógicas en una vista del origen de datos &#40;Analysis Services&#41;](define-logical-relationships-in-a-data-source-view-analysis-services.md).  
  
     El ejemplo siguiente confirma que las tablas utilizadas en este procedimiento están vinculadas mediante claves principales.  
  
     ![Mostrar tablas relacionadas de DSV](../media/ssas-m2m-dsvpkeys.PNG "DSV que muestra las tablas relacionadas")  
  
#### <a name="step-2-create-dimensions-and-measure-groups"></a>Paso 2: crear dimensiones y grupos de medida  
  
1.  En SQL Server Data Tools, en un proyecto multidimensional, haga clic con el botón derecho en **Dimensiones** y seleccione **Nueva dimensión**.  
  
2.  Cree una dimensión nueva basada en la tabla existente **DimSalesReason**. Acepte todos los valores predeterminados al especificar el origen.  
  
     En los atributos, selecciónelos todos.  
  
     ![Lista de atributos en nueva dimensión](../media/ssas-m2m-dimsalesreason.PNG "lista de atributos en nueva dimensión")  
  
3.  Cree una segunda dimensión basada en la tabla existente Fact Internet Sales. Aunque se trata de una tabla de hechos, contiene información de Pedido de venta. La usaremos para crear una dimensión Sales Order.  
  
4.  En Especificar información de origen, verá una advertencia que indica que se debe especificar una columna Nombre. Elija **SalesOrderNumber** como nombre.  
  
     ![Dimensión Sales Order que muestra la columna nombre](../media/ssas-m2m-dimsalesordersource.PNG "dimensión Sales Order que muestra la columna de nombre")  
  
5.  En la página siguiente del asistente, elija los atributos. En este ejemplo, puede seleccionar simplemente **SalesOrderNumber**.  
  
     ![Lista de atributos de pedido de ventas dimensión mostrando](../media/ssas-m2m-dimsalesorderattrib.PNG "dimensión mostrando atributo lista de ventas")  
  
6.  Cambie el nombre de la dimensión a **Dim Sales Orders**, para que tenga una convención de nomenclatura coherente para las dimensiones.  
  
     ![Página del asistente que muestra el cambio de nombre de dimensión](../media/ssas-m2m-dimsalesorders.PNG "página del asistente que muestra el cambio de nombre de dimensión")  
  
7.  Haga clic con el botón derecho en **Cubos** y seleccione **Nuevo cubo**.  
  
8.  En las tablas de grupo de medida, elija **FactInternetSales** y **FactInternetSalesReason**.  
  
     Elige **FactInternetSales** porque contiene las medidas que desea usar en el cubo. Elige **FactInternetSalesReason** porque es el grupo de medida intermedio que proporciona datos de asociación de miembros que relaciona los pedidos de venta con las razones de venta.  
  
9. Elija medidas para cada tabla de hechos.  
  
     Para simplificar el modelo, borre todas las medidas y, luego, seleccione solamente **Sales Amount** y **Fact Internet Sales Count** en la parte inferior de la lista. **FactInternetSalesReason** tiene solo una medida, por lo que se selecciona automáticamente.  
  
10. En la lista de dimensiones, debe ver **Dim Sales Reason** y **Dim Sales Orders**.  
  
     En la página Seleccionar nuevas dimensiones, el asistente le preguntará si desea crear una dimensión nueva para **Fact Internet Sales Dimension**. No necesita esta dimensión, por lo que puede quitarla de la lista.  
  
11. Asigne nombre al cubo y haga clic en **Finalizar**.  
  
#### <a name="step-3-define-many-to-many-relationship"></a>Paso 3: definir la relación de varios a varios  
  
1.  En el Diseñador de cubos, haga clic en la pestaña Uso de dimensiones. Observe que ya hay una relación de varios a varios entre **Dim Sales Reason** y **Fact Internet Sales**. Recuerde que el icono siguiente indica una relación de varios a varios.  
  
     ![Icono de varios a varios en el uso de dimensiones](../media/ssas-m2m-icondimusage.png "-to-many icono en el uso de dimensiones")  
  
2.  Haga clic en la celda que es la intersección entre **Dim Sales Reason** y **Fact Internet Sales**y, luego, haga clic en el botón para abrir el cuadro de diálogo Definir relación.  
  
     Puede ver que este cuadro de diálogo se usa para especificar una relación de varios a varios. Si fuera a agregar en su lugar dimensiones que tuvieran una relación normal, usaría este cuadro de diálogo para cambiarla a una relación de varios a varios.  
  
     ![Botón de la relación de definir en el uso de dimensiones](../media/ssas-m2m-btndimusage.png "botón Definir relación en el uso de dimensiones")  
  
3.  Implemente el proyecto en una instancia multidimensional de Analysis Services. En el paso siguiente, examinará el cubo en Excel para comprobar sus comportamientos.  
  
## <a name="testing-many-to-many"></a>Probar relaciones de varios a varios  
 Cuando se define una relación de varios a varios en un cubo, es obligatorio asegurarse de que las consultas devuelven los resultados esperados. Debe probar el cubo con la herramienta de la aplicación cliente que usarán los usuarios finales. En el procedimiento siguiente, usará Excel para conectarse al cubo y comprobar los resultados de la consulta.  
  
#### <a name="browse-the-cube-in-excel"></a>Examinar el cubo en Excel  
  
1.  Implemente el proyecto y examine el cubo para confirmar que las agregaciones son válidas.  
  
2.  En Excel, haga clic en **Datos** | **De otros orígenes** | **De Analysis Services**. Especifique el nombre del servidor, y elija la base de datos y el cubo.  
  
3.  Cree una tabla dinámica que use lo siguiente:  
  
    -   **Sales Amount** como valor  
  
    -   **Sales Reason Name** en columnas  
  
    -   **Sales Order Number** en Filas  
  
4.  Analice los resultados. Como estamos usando datos de ejemplo, la impresión inicial es que todos los pedidos de ventas tienen valores idénticos. Sin embargo, si se desplaza hacia abajo, empieza a ver variaciones en los datos.  
  
     Un poco hacia abajo puede ver el importe y las razones de ventas del número de pedido **SO5382**. El total general de este pedido concreto es **539,99**y entre las razones se compra atribuidas a este pedido se incluyen Promotion, Other y Price.  
  
     ![Hoja de cálculo de Excel que muestra agregaciones varios a varios](../media/ssas-m2m-excel.png "hoja de cálculo de Excel que muestra agregaciones varios a varios")  
  
     Observe que el importe de Sales Amount se calculó correctamente para el pedido; es **539,99** para todo el pedido. Aunque se indica **539,99** para todas las razones, ese valor no se sumó para las tres razones, lo que infla erróneamente nuestro total general.  
  
     En primer lugar, ¿por qué incluir un importe de ventas bajo cada razón de venta? La respuesta es que nos permite identificar el importe de ventas que podemos atribuir a cada razón.  
  
5.  Desplácese hasta el final de la hoja de cálculo. Ahora es fácil ver que el precio es la razón más importante de las compras de los clientes con respecto a las demás razones y al total general.  
  
     ![Libro de Excel que muestra los totales de varios a varios](../media/ssas-m2m-excelgrandtotal.png "libro de Excel que muestra los totales de varios a varios")  
  
#### <a name="tips-for-handling-unexpected-query-results"></a>Sugerencias para controlar resultados inesperados de la consulta  
  
1.  Oculte las medidas del grupo de medida intermedio, como el recuento, que no devuelvan resultados significativos en una consulta. Esto impide que la gente intente usar agregaciones que produzcan datos sin sentido. Para ocultar una medida, establezca **Visibilidad** en **False** en el atributo del Diseñador de dimensiones.  
  
2.  Cree perspectivas para usar un subconjunto de medidas y dimensiones que admitan la experiencia de análisis que desea proporcionar. Puede que un cubo que contiene muchos grupos de medidas y dimensiones no sea adecuado en todos los casos. Al aislar las dimensiones y los grupos de medida que piensa usar conjuntamente, se asegura de obtener un resultado más predecible.  
  
3.  Recuerde siempre realizar la implementación y volver a conectarse después de cambiar un modelo. En Excel, use el botón Actualizar de la cinta Analizar tabla dinámica.  
  
4.  Evite usar grupos de medida vinculada en diversas relaciones varios a varios, especialmente cuando estas relaciones están en distintos cubos. Si lo hace, puede producir agregaciones ambiguas. Para más información, vea [Cantidades incorrectas para medidas vinculadas en cubos que contienen relaciones varios a varios](http://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx).  
  
##  <a name="bkmk_Learn"></a> Learn more  
 Use los vínculos siguientes para obtener información adicional que le ayude a dominar estos conceptos.  
  
 [Cómo definir una dimensión varios a varios en Analysis Services](http://go.microsoft.com/fwlink/?LinkId=324759)  
  
 [La revolución varios a varios 2.0](http://go.microsoft.com/fwlink/?LinkId=324760)  
  
 [Tutorial: Ejemplo de dimensiones varios a varios para SQL Server Analysis Services](http://go.microsoft.com/fwlink/?LinkId=324761)  
  
## <a name="see-also"></a>Vea también  
 [Relaciones de dimensión](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Instalar los datos de ejemplo y proyectos para el Tutorial de modelado Multidimensional de Analysis Services](../install-sample-data-and-projects.md)   
 [Implementar proyectos de Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)   
 [Perspectivas de modelos multidimensionales](perspectives-in-multidimensional-models.md)  
  
  
