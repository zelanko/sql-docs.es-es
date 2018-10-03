---
title: Conceder acceso personalizado a datos de dimensión (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.dimensiondata.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- AllowedSet property
- IsAllowed property
- DeniedSet property
- user access rights [Analysis Services], dimensions
- custom dimension data access [Analysis Services]
- permissions [Analysis Services], dimensions
- DefaultMember property
- VisualTotals property
- ApplyDenied property
ms.assetid: b028720d-3785-4381-9572-157d13ec4291
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 51e180d39df78a90869c2d6cdfc366e0cc13ba02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091745"
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>Conceder acceso personalizado a datos de dimensión (Analysis Services)
  Después de permitir el acceso de lectura a un cubo, puede establecer permisos adicionales que permitan o denieguen explícitamente el acceso a miembros de la dimensión (incluidas las medidas que contiene la Dimensión de Medidas que contengan todas las medidas utilizadas en un cubo). Por ejemplo, si hay varias categorías de distribuidores, conviene establecer permisos para excluir datos de un tipo de negocio específico. La ilustración siguiente representa el antes y el después a la denegación de acceso al tipo de negocio Warehouse en la dimensión Reseller.  
  
 ![Las tablas dinámicas con y sin un miembro de dimensión](../media/ssas-permsdimdenied.png "tablas dinámicas con y sin un miembro de dimensión")  
  
 De forma predeterminada, si puede leer datos de un cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , automáticamente cuenta con permisos de lectura en todas las medidas y miembros de dimensión asociados a ese cubo. Mientras que es posible que este comportamiento sea suficiente para múltiples escenarios, en ocasiones los requisitos de seguridad requieren una estrategia de autorización más segmentada, con diferentes niveles de acceso para los distintos usuarios, en la misma dimensión.  
  
 Puede restringir el acceso si elige los miembros a los que permitir (AllowedSet) o denegar (DeniedSet) el acceso. Para ello, seleccione o anule la selección de los miembros de la dimensión que vaya a incluir o excluir del rol.  
  
 La seguridad básica de las dimensiones es más sencilla; basta con seleccionar los atributos de dimensión y las jerarquías de atributo que quiera incluir o excluir del rol. La seguridad avanzada resulta más compleja y requiere conocimientos expertos en la generación de scripts MDX. Ambos enfoques se describen a continuación.  
  
## <a name="prerequisites"></a>Requisitos previos  
 No todas las medidas o miembros de dimensión se pueden usar en escenarios de acceso personalizados. Si hay un rol que restringe el acceso a una medida o miembro predeterminado o a medidas que forman parte de expresiones de medida, se producirá un error en la conexión.  
  
 **Busque obstrucciones en la seguridad de dimensiones: medidas predeterminadas, miembros predeterminados y medidas usadas en expresiones de medida**  
  
1.  En SQL Server Management Studio, haga clic con el botón derecho en un cubo y seleccione **Incluir cubo como** | **ALTER para** | **Nueva ventana del Editor de consultas**.  
  
2.  Busque `DefaultMeasure`. Debería encontrar una para el cubo y una para cada perspectiva. Al definir la seguridad de dimensiones, evite restringir el acceso a las medidas predeterminadas.  
  
3.  A continuación, busque `MeasureExpression`. Una expresión de medida es una medida basada en un cálculo que suele incluir otras medidas. Compruebe que la medida que quiere restringir no se usa en una expresión. También puede seguir adelante y restringir el acceso, siempre que se asegure de excluir todas las referencias a esa medida en el cubo.  
  
4.  Finalmente, busque `DefaultMember`. Tome nota de cualquier atributo que sirva como miembro predeterminado de un atributo. Evite colocar restricciones en esos atributos a la hora de configurar la seguridad de dimensiones.  
  
## <a name="basic-dimension-security"></a>Seguridad básica de dimensiones  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Roles** para la base de datos correspondiente en el Explorador de objetos y, después, haga clic en un rol de base de datos (o cree un rol de base de datos).  
  
     El rol ya debe disponer de acceso de lectura al cubo. Vea [Grant cube or model permissions &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) si necesita ayuda con este paso.  
  
2.  En **Datos de dimensiones** | **Básico**, seleccione la dimensión para la que vaya a establecer permisos.  
  
3.  Elija la jerarquía de atributos. No estarán disponibles todos los atributos. Solamente los atributos con **AttributeHierarchyEnabled** aparecen en la lista **Jerarquía de atributos** .  
  
4.  Elija los miembros a los que permitir o denegar el acceso. La opción predeterminada es permitir el acceso a través de **Seleccionar todos los miembros** . Se recomienda mantener esta opción predeterminada y posteriormente desactivar la selección de miembros individuales que no deben estar visibles en las cuentas de usuario y grupo de Windows en el panel **Pertenencia** a través de este rol. La ventaja es que los miembros nuevos que se agregan en operaciones de procesamiento posteriores estarán automáticamente disponibles para las personas que se conecten a este rol.  
  
     También puede **Anular la selección de todos los miembros** para revocar el acceso global y, después, elegir los miembros a los que se permitirá el acceso. En futuras operaciones de procesamiento, los nuevos miembros no estarán visibles hasta que edite manualmente la seguridad de los datos de las dimensiones para permitir el acceso a los mismos.  
  
5.  Si lo desea, haga clic en **avanzadas** para habilitar `Visual Totals` para esta jerarquía de atributo. Esta opción vuelve a calcular las agregaciones en función de los miembros disponibles en el rol.  
  
    > [!NOTE]  
    >  Cuando se aplican permisos que eliminan miembros de una dimensión, los totales agregados no se recalculan de forma automática. Supongamos que el `All` miembro de una jerarquía de atributo devuelve un recuento de 200 antes de que se aplican los permisos. Después de aplicar los permisos que deniegan el acceso a algunos miembros, `All` todavía devuelve 200, aunque los valores de miembro visibles para el usuario son muchos menos. Para evitar confundir a los consumidores del cubo, puede configurar el `All` miembro sean la agregación de esos miembros para que los miembros del rol, en lugar de la suma de todos los miembros de la jerarquía de atributo. Para invocar este comportamiento, puede habilitar `Visual Totals` en el **avanzadas** tabulación al configurar la seguridad de dimensión. Una vez que lo haya habilitado, el agregado se calcula en tiempo de consulta en lugar de recuperarse a partir de agregados previamente calculados. Esto puede tener una repercusión apreciable en el rendimiento de la consulta, por tanto, úselo únicamente cuando sea necesario.  
  
## <a name="hiding-measures"></a>Ocultar medidas  
 En [Grant custom access to cell data &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md), se explicó que para ocultar totalmente todos los aspectos visuales de una medida, y no solamente los datos de la celda, se requieren permisos para los miembros de la dimensión. En esta sección, se describe cómo denegar el acceso a los metadatos del objeto de una medida.  
  
1.  En **Datos de dimensiones** | **Básico**, desplácese en dirección descendente por la lista de dimensiones hasta llegar a las dimensiones de los cubos y seleccione **Dimensión de medidas**.  
  
2.  En la lista de medidas, desactive la casilla para las medidas que no deben aparecer para los usuarios que se conecten a través de este rol.  
  
> [!NOTE]  
>  Consulte los requisitos previos para saber cómo identificar medidas que pueden romper la seguridad del rol.  
  
## <a name="advanced-dimension-security"></a>Seguridad de dimensión avanzada  
 Si tiene conocimientos expertos de MDX, otro método consiste en escribir expresiones MDX que establezcan criterios según los cuales se permita o deniegue el acceso a los miembros. Haga clic en **Crear rol** | **Datos de dimensión** | **Avanzadas** para proporcionar el script.  
  
 Puede usar el Generador MDX para escribir instrucciones MDX. Vea [Generador MDX &#40;Analysis Services - Datos multidimensionales&#41;](../mdx-builder-analysis-services-multidimensional-data.md) para obtener más información. La pestaña **Avanzada** presenta las siguientes opciones:  
  
 **Atributo**  
 Seleccione el atributo para el que desea administrar la seguridad de los miembros.  
  
 **Conjunto de miembros permitido**  
 El elemento AllowedSet puede dar como resultado ningún miembro (predeterminado), todos los miembros o algunos miembros. Si permite el acceso a un atributo y no define ningún miembro del conjunto permitido, se concede acceso a todos los miembros. Si permite acceso a un atributo y define un conjunto específico de miembros de atributos, solo estarán visibles los miembros permitidos explícitamente.  
  
 Si se crea un elemento AllowedSet, tendrá un efecto dominó cuando el atributo participe en una jerarquía de varios niveles. Por ejemplo, un caso en el que el rol permite el acceso al estado de Washington (una situación en la que el rol otorga permisos a la división comercial de Washington de una empresa). Para las personas que se conecten a través de este rol, las consultas que incluyan antecesores (Estados Unidos) o descendentes (Seattle y Redmond) solamente verán miembros en una cadena que incluye el estado de Washington. Dado que no se han permitido de forma explícita otros estados, el efecto será el mismo que si se hubieran denegado.  
  
> [!NOTE]  
>  Si define un conjunto vacío ({}) de los miembros de atributo, ningún miembro del atributo estará visible para el rol de base de datos. La ausencia de un conjunto permitido no se interpreta como un conjunto vacío.  
  
 **Conjunto de miembros denegado**  
 La propiedad DeniedSet puede dar como resultado ningún miembro, todos los miembros (predeterminado) o algunos miembros del atributo. Cuando el conjunto que se ha denegado contiene únicamente un conjunto específico de miembros de atributo, el rol de base datos deniega el acceso solo a los miembros específicos, así como a los descendentes si el atributo es una jerarquía de múltiples niveles. Sigamos con el ejemplo de la división comercial en el estado de Washington. Si Washington se coloca en DeniedSet, las personas que se conecten a través de este rol verán el resto de estados salvo Washington y sus atributos descendentes.  
  
 Recuerde que según se indicó en la sección anterior, el conjunto denegado es una colección de tamaño fijo. Si al procesarse más veces se incorporan miembros nuevos, también tendrán el acceso denegado; tendrá que editar este rol para agregar a esos miembros a la lista.  
  
 **Miembro predeterminado**  
 La propiedad DefaultMember establece el conjunto de datos que se devuelve a un cliente cuando un atributo no se incluye explícitamente en una consulta. Cuando el atributo no se incluye explícitamente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza uno de los siguientes miembros predeterminados para el atributo:  
  
-   Si el rol de base de datos define un miembro predeterminado para el atributo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza este miembro predeterminado.  
  
-   Si el rol de base de datos no define un miembro predeterminado para el atributo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza el miembro predeterminado que se define para el atributo en sí. El miembro predeterminado para un atributo, a menos que se especifique lo contrario, es el miembro `All` (excepto si el atributo se define como no agregable).  
  
 Por ejemplo, supongamos que un rol de base de datos especifica `Male` como miembro predeterminado para el atributo `Gender`. A menos que una consulta incluya explícitamente el atributo `Gender` y especifique un miembro diferente para este atributo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devolverá un conjunto de datos que solamente incluye a los clientes masculinos. Para obtener más información sobre cómo establecer el miembro predeterminado, vea [Definir un miembro predeterminado](attribute-properties-define-a-default-member.md).  
  
 **Habilitar total visual**  
 La propiedad VisualTotals indica si los valores de celdas agregados que se muestran se calculan en función de todos los valores de celda o únicamente en función de los valores de celda que están visibles para el rol de base de datos.  
  
 De forma predeterminada, la propiedad VisualTotals está deshabilitada (establecida en `False`). Esta configuración predeterminada maximiza el rendimiento porque [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede calcular rápidamente el total de todos los valores de celda, en vez de tener que dedicar tiempo a seleccionar qué valores de celda calcular.  
  
 Pero si la propiedad VisualTotals está deshabilitada, se podría producir un problema de seguridad si un usuario puede usar los valores de celdas agregados para deducir los valores para miembros de atributos a los que el rol de base de datos del usuario no tiene acceso. Por ejemplo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza los valores para tres miembros del atributo a fin de calcular un valor de celdas agregado. El rol de base de datos puede ver dos de estos tres miembros de atributo. Usando el valor de celdas agregado, un miembro de este rol de base de datos podría deducir el valor para el tercer miembro del atributo.  
  
 Establecer la propiedad VisualTotals en `True` puede eliminar este riesgo. Si habilita la propiedad VisualTotals, un rol de base de datos solamente puede ver totales agregados para los miembros de dimensión para los que tiene permiso el rol.  
  
 **Comprobación**  
 Haga clic en esta opción para probar la sintaxis MDX que se define en esta página.  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos para cubos o modelos &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acceso personalizado a datos de la celda &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)   
 [Conceder permisos en las estructuras de minería de datos y modelos &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder permisos en un objeto de origen de datos &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
