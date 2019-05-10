---
title: Introducción a Master Data Services (MDS) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- what is master data
helpviewer_keywords:
- Master Data Services, overview
- Master Data Services
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3514f15156de2856be6e13b0df29affa23e78303
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489742"
---
# <a name="master-data-services-overview-mds"></a>Introducción a Master Data Services (MDS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tema se describen las características de administración y organización de datos principales de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. 
  
 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] le permite administrar un conjunto principal de los datos de su organización. Puede organizar los datos en modelos, crear reglas para actualizar los datos y controlar quién actualiza los datos. Puede usar Excel para compartir el conjunto de datos maestros con otras personas de su organización. 
  
 >  Para obtener una descripción de la arquitectura de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] , consulte el artículo [Master Data Services: conceptos básicos](https://www.simple-talk.com/sql/database-delivery/master-data-services-basics) en simple-talk.com. Para obtener información sobre las nuevas características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Novedades en Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
   **Para obtener instrucciones sobre cómo instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], configurar la base de datos y el sitio web e implementar los modelos de ejemplo, consulte** [Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md).  
  
 En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], el modelo es el contenedor de nivel superior de la estructura de datos maestros. Cree un modelo para administrar grupos de datos similares, por ejemplo, para administrar los datos de productos en línea. Un modelo contiene una o más entidades y las entidades contienen miembros que son los registros de datos. Una entidad es similar a una tabla.  
  
 Por ejemplo, el modelo de producto en línea puede contener entidades como producto, color y estilo. La entidad de color puede contener miembros para los colores rojo, plata y negro.  
  
 ![Entidad de color](../master-data-services/media/mds-productmodel-colorentity-composite.png "Entidad de color")  
  
 Los modelos también contienen atributos que se definen dentro de las entidades. Un atributo contiene valores que ayudan a describir los miembros de entidad. Hay atributos de forma libre y otros basados en dominio.  Un atributo basado en dominio contiene valores que rellenan los miembros de una entidad y que pueden usarse como valores de atributo para otras entidades.  
  
 Por ejemplo, la entidad Producto podría tener los atributos de forma libre Costo y Peso. Además, hay un atributo basado en dominio para el color ![Número 1](../master-data-services/media/mds-number1.png "Número 1") que contiene valores que se rellenan con los miembros de la entidad de color. Esta lista maestra de colores se usa como valores de atributo para la entidad Producto ![Número 2](../master-data-services/media/mds-number2.png "Número 2").  
  
 ![Atributo basado en dominio para el color](../master-data-services/media/mds-productentity-color-domainattribute.png "Atributo basado en dominio para el color")  
  
 Las jerarquías derivadas proceden de las relaciones entre entidades en un modelo. Estas son las relaciones de atributo basado en dominio. Por ejemplo, en el modelo de producto, puede tener una jerarquía derivada de color ![Número 1](../master-data-services/media/mds-number1.png "Número 1") que proceda de la relación entre las entidades de color ![Número 2](../master-data-services/media/mds-number2.png "Número 2") y producto ![Número 3](../master-data-services/media/mds-number3.png "Número 3").  
  
 ![Jerarquía derivada de color](../master-data-services/media/mds-derivedhierarchy.png "Jerarquía derivada de color")  
  
 Una vez que haya definido una estructura básica para los datos, puede empezar a agregar registros de datos (miembros) mediante la característica de importación. Cargue datos en las tabla de almacenamiento provisional, valide los datos con reglas de negocios y cárguelos en tablas de MDS.  También puede utilizar las reglas de negocios para establecer los valores de atributo.  
  
 En la tabla siguiente se describen las tareas clave [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . A menos que se indique lo contrario, todos los procedimientos siguientes requieren que sea administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
> [!NOTE]  
>  Puede ser aconsejable que complete las siguientes tareas en un entorno de prueba y que use los datos de ejemplo proporcionados al instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obtener más información, consulte [Implementar modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md).  
  
|Acción|Detalles|Temas relacionados|  
|------------|-------------|--------------------|  
|Crear un modelo|Al crear un modelo, se considera VERSION_1.|[Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)<br /><br /> [Crear un modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)|  
|Crear entidades|Cree tantas entidades como necesite para contener los miembros.|[Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)<br /><br /> [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|Crear entidades para utilizar como atributos basados en dominio|Para crear un atributo basado en dominio, primero cree la entidad para rellenar la lista de valores de atributo.|[Atributos basados en dominios &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|Crear atributos para las entidades|Cree atributos para describir los miembros. El atributo Code y Name se incluyen automáticamente en cada entidad y no se pueden quitar. Puede que desee crear otros atributos de forma libre para contener texto, fechas, números o archivos.|[Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)<br /><br /> [Crear un atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [Crear un atributo numérico &#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [Crear un atributo de fecha &#40;Master Data Services&#41;](../master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [Crear un atributo de vínculo &#40;Master Data Services&#41;](../master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [Crear un atributo de archivo &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|Crear grupos de atributos|Si tiene más de cuatro o cinco atributos para una entidad, puede ser aconsejable crear grupos de atributos. Estos grupos son las pestañas que se muestran sobre la cuadrícula en el **Explorador** y facilitan la navegación agrupando los atributos en pestañas individuales.|[Grupos de atributos &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)<br /><br /> [Crear un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Importar miembros para las entidades de apoyo|Importe los datos para las entidades compatibles mediante el uso del proceso de almacenamiento provisional. En el caso del modelo Producto, esto podría significar importar colores o tamaños. También puede crear miembros manualmente.<br /><br /> <br /><br /> Nota: Los usuarios pueden crear miembros en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] si tienen el permiso **Actualizar**, como mínimo, para el objeto de modelo de hoja de una entidad y acceso al área funcional del **Explorador**.|[Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)<br /><br /> [Crear un miembro hoja &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Crear y aplicar reglas de negocios para garantizar la calidad de los datos|Cree y publique reglas de negocios para asegurarse de la exactitud de los datos. Puede utilizar las reglas de negocios para:<br /><br /> Establecer los valores de atributo predeterminados.<br /><br /> Cambiar los valores de atributo.<br /><br /> Enviar notificaciones por correo electrónico cuando los datos no superan la validación de la regla de negocios.|[Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)<br /><br /> [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [Validar miembros específicos con las reglas de negocios (Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)<br /><br /> [Configurar notificaciones por correo electrónico &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Importar miembros para las entidades principales y aplicar reglas de negocios|Importe los miembros para las entidades principales utilizando el proceso provisional. Cuando termine, valide la versión, que aplica reglas de negocios a todos los miembros en la versión del modelo.<br /><br /> A continuación, puede trabajar para corregir los problemas de validación de reglas de negocios.|[Validación &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)<br /><br /> [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [Procedimiento almacenado de validación &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)|  
|Crear jerarquías derivadas|Estas jerarquías derivadas pueden actualizarse a medida que la empresa cambie y garantizan que todos los miembros se tienen en cuenta en el nivel adecuado.|[Jerarquías derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [Crear una jerarquía derivada &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Si es necesario, crear jerarquías explícitas|Si desea crear jerarquías que no se basen en niveles y que incluyan miembros de una sola entidad, puede crear jerarquías explícitas.|[Jerarquías explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [Crear una jerarquía explícita &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Si es necesario, crear colecciones|Si desea ver agrupaciones diferentes de miembros para notificación o análisis, y no necesita una jerarquía completa, cree una colección.<br /><br /> <br /><br /> Nota: Los usuarios pueden crear colecciones en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] si tienen el permiso **Actualizar**, como mínimo, para el objeto de modelo de colección y acceso al área funcional del **Explorador**.|[Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)<br /><br /> [Crear una colección &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|Crear metadatos definidos por el usuario|Para describir los objetos de modelo, agregue los metadatos definidos por el usuario al modelo. Los metadatos podrían incluir el propietario de un objeto o el origen del que proceden los datos.||  
|Bloquear una versión del modelo y asignar una marca de versión|Bloquee una versión del modelo para evitar cambios en los miembros, excepto los realizados por los administradores. Cuando los datos de la versión se han validado correctamente con las reglas de negocios, puede confirmar la versión, lo que evita los cambios en los miembros realizados por todos los usuarios.<br /><br /> Cree y asigne una marca de versión al modelo. Las marcas ayudan a los usuarios y sistemas de suscripción a identificar la versión del modelo que utilizan.|[Versiones &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)<br /><br /> [Bloquear una versión &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)<br /><br /> [Crear una marca de versión &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)|  
|Crear vistas de suscripción|Para que los sistemas de suscripción usen sus datos maestros, cree vistas de suscripción, que crean vistas estándar en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Información general: exportación de datos &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)<br /><br /> [Crear una vista de suscripciones para exportar datos &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Configurar los permisos de usuario y de grupo|No puede copiar los permisos de usuario y de grupo de una prueba en un entorno de producción. Sin embargo, puede utilizar su entorno de pruebas para determinar la seguridad que desea utilizar posteriormente en producción.|[Seguridad &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)<br /><br /> [Agregar un grupo &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)<br /><br /> [Agregar un usuario &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)|  
  
 Cuando esté listo, puede implementar su modelo, con o sin sus datos, en el entorno de producción. Para obtener más información, consulte [Implementar modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md).  
  
  

