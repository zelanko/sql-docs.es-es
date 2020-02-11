---
title: Página seguridad de elemento de modelo (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.modelitemsecurity.f1
ms.assetid: 8c5b29ae-1f17-41f2-ab59-97899b8fb4fc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f45169a2fdc8fdc4d56cb27a8bf6348a3c3c1a29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108229"
---
# <a name="model-item-security-page-report-manager"></a>Página Seguridad de elemento de modelo (Administrador de informes)
  Use esta página para proteger partes de un modelo concediendo o revocando permisos de solo lectura en elementos concretos. La seguridad del elemento de modelo afecta a la exploración de datos ad hoc en tiempo de ejecución y a la capacidad de usar partes de un modelo publicado cuando se crean informes en el Generador de informes. Para usar esta característica, debe tener permisos de Administrador de contenido.  
  
 La seguridad del elemento de modelo se aplica a un modelo procesado en el servidor de informes y no afecta a los archivos .smdl que se modifican en el Diseñador de modelos o se usan en el Diseñador de informes. Además, no tiene ningún efecto en los usuarios que tienen permiso para modificar una definición de modelo. Los usuarios que tienen permisos de publicador o de administrador de contenido en un modelo pueden ver todas las partes del mismo, con independencia de que se aplique la seguridad del elemento de modelo.  
  
> [!NOTE]  
>  Los elementos de modelo se pueden proteger más mediante el uso de filtros de seguridad.  
  
 Puede definir la seguridad de elementos de modelo en las entidades, carpetas y campos individuales de un modelo. Dado que un modelo presenta este tipo de superficie grande de elementos protegibles, la herencia de permisos está integrada en el modelo de manera que pueda proteger un gran número de elementos a través de un número relativamente pequeño de asignaciones de roles. La herencia de permisos se basa en lo siguiente:  
  
-   Modelo  
  
-   Nodo raíz  
  
-   Carpetas o entidades  
  
-   Fields  
  
 Inicialmente, el permiso para tener acceso a los elementos de modelo se hereda a través de las asignaciones de roles que se establecen en el propio modelo. Un usuario que tiene permiso para ver un modelo de una carpeta en el Administrador de informes puede ver todos los elementos del modelo.  
  
 Si aplica la seguridad de elemento de modelo, debe crear al menos una asignación de roles en el nodo raíz. Esta asignación de roles inicial en el nodo raíz se convierte en el nuevo origen de permisos heredados. Todos los elementos de la jerarquía de modelo heredan automáticamente la asignación de roles en el nodo raíz.  
  
 Para personalizar aún más los permisos en la exploración de datos, puede variar los permisos en las carpetas y entidades. Finalmente, puede establecer permisos en campos individuales.  
  
 Para facilitar el mantenimiento de las asignaciones de roles, establezca solamente los permisos en carpetas o entidades en lugar de en campos individuales. No puede buscar las asignaciones de roles que crea. Si establece la seguridad en campos específicos y, posteriormente, desea actualizar la configuración de seguridad, debe hacer clic en el espacio de nombres del modelo para buscar los campos que ha protegido.  
  
 Para empezar, cree una asignación de roles en el nodo raíz y, a continuación, cree asignaciones de roles adicionales en las entidades y carpetas. Para borrar la seguridad de elemento de modelo, desactive la casilla **Proteger cada uno de los elementos de modelo de forma independiente para este modelo**. Al desactivar la casilla, se recuperan los permisos iniciales heredados del modelo.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Para abrir la página Propiedades generales de un informe  
  
1.  Abra el Administrador de informes y busque el modelo del que desea ver o configurar la seguridad para los elementos de modelo.  
  
2.  Mantenga el mouse sobre el modelo y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página Propiedades generales correspondiente al modelo.  
  
4.  Seleccione la pestaña **Seguridad de elemento de modelo** .  
  
## <a name="options"></a>Opciones  
 **Proteger cada uno de los elementos de modelo de forma independiente para este modelo**  
 Haga clic en esta casilla para habilitar la seguridad de elemento de modelo.  
  
 **Especifique la seguridad para los distintos elementos existentes en el modelo**  
 Muestra todos los elementos de un modelo. Puede navegar por el espacio de nombres del modelo para seleccionar el elemento que desea proteger. Solo puede seleccionar un elemento cada vez. Asegúrese de crear la primera asignación de roles en el nodo raíz antes de continuar con otras entidades y carpetas.  
  
 **Heredar permisos del elemento primario**  
 Haga clic en esta opción para heredar la configuración de seguridad del elemento primario.  
  
 **Asignar permiso de lectura a los usuarios y grupos siguientes (separados con puntos y coma)**  
 Haga clic en esta opción para especificar la cuenta de usuario o grupo para la que define el acceso. Si va a utilizar la seguridad predeterminada, las cuentas de usuario y grupo son las cuentas de dominio de Windows. Especifique las cuentas con este formato: * \<>\\ de dominio<\>cuenta*.  
  
## <a name="see-also"></a>Consulte también  
 [Servidor de informes en Management Studio (Ayuda F1)](tools/report-server-in-management-studio-f1-help.md)  
  
  
