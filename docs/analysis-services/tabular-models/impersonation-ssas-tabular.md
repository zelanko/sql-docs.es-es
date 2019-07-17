---
title: Suplantación en los modelos tabulares de Analysis Services | Microsoft Docs
ms.date: 01/21/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 981b98523a53e0c828de5e9cdf8a6c35c6843805
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207650"
---
# <a name="impersonation"></a>Suplantación 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artículo proporciona una descripción de cómo las credenciales de inicio de sesión se utiliza por Analysis Services cuando se conecta a un origen de datos para importar y procesar (actualizar) los datos de autores de modelos tabulares.  

##  <a name="bkmk_conf_imp_info"></a> Configurar la suplantación  
 Donde y en qué contexto existe un modelo determina cómo se configura la información de suplantación. Al crear un nuevo proyecto de modelo, la suplantación está configurada en SQL Server Data Tools (SSDT) al conectarse a un origen de datos para importar datos. Una vez implementado un modelo, la suplantación puede configurarse en una propiedad de cadena de conexión de base de datos de modelo mediante el uso de SQL Server Management Studio (SSMS). Para los modelos tabulares en Azure Analysis Services, puede usar SSMS o **ver como: Secuencia de comandos** modo en el diseñador basado en explorador para editar el archivo Model.bim en JSON.
  
##  <a name="bkmk_how_imper"></a> ¿Cómo se utiliza la suplantación  
 La*suplantación* es la capacidad de una aplicación de servidor, como Analysis Services, de asumir la identidad de una aplicación cliente. Analysis Services se ejecuta con una cuenta de servicio; sin embargo, cuando el servidor establece una conexión a un origen de datos, utiliza la suplantación para que las comprobaciones de acceso para la importación de datos y el procesamiento puede realizarse.  
  
 Son diferentes de las credenciales que iniciado sesión actualmente en con las credenciales usadas para la suplantación. Las credenciales de usuario de inicio de sesión se utiliza para las operaciones de cliente determinadas al crear un modelo.  
  
 Es importante para comprender cómo se especifican y protegen, así como la diferencia entre los contextos en que tanto sus con signo en las credenciales de suplantación se usan las credenciales de usuario y cuando se usan otras credenciales de suplantación.  
  
 **Descripción de las credenciales de servidor**  
 
Cuando se importan o procesan datos, las credenciales de suplantación se usan para conectarse al origen de datos y capturar los datos. Esta conexión es un *servidor* operación que se ejecuta en el contexto de una aplicación cliente porque el servidor de Analysis Services que hospeda la base de datos del área de trabajo se conecta al origen de datos y captura los datos.  
  
 Al implementar un modelo en un servidor de Analysis Services, si la base de datos del área de trabajo está en la memoria cuando se implementa el modelo, las credenciales se pasan al servidor de Analysis Services en el que se implementa el modelo. Las credenciales de usuario nunca están almacenados en disco.  
  
 Cuando un modelo implementado procesa los datos desde un origen de datos, las credenciales de suplantación, almacenadas en la base de datos en memoria, se usan para conectarse al origen de datos y capturar los datos. Dado que este proceso se controla mediante la administración de la base de datos de modelo de servidor de Analysis Services, esta conexión nuevo es una operación de servidor.  
  
 **Descripción de las credenciales de cliente**  
  
 Al crear un nuevo modelo o agregar un origen de datos a un modelo existente, conectarse a un origen de datos y seleccionar tablas y vistas que se importarán en el modelo. En el Asistente para importación de tablas o el Diseñador de Data\Query obtener vista previa y filtrar las características de, ve un ejemplo de los datos que importa. También puede especificar filtros para excluir los datos que no es necesario en el modelo.  
  
 De forma similar, para los modelos que ya se han creado, use el **propiedades de la tabla** cuadro de diálogo Vista previa y filtrar datos importados en una tabla.  
  
 Las características de vista previa y filtrar, **propiedades de la tabla**, y **Partition Manager** cuadros de diálogo están en proceso *del lado cliente* operación; es decir, lo que se realiza durante la ejecución operación son diferentes de cómo se conecta el origen de datos a y desde el origen de datos; los datos se capturan una operación del lado servidor. Las credenciales usadas para la vista previa y filtrar los datos son las credenciales de usuario que inició sesión. En efecto, sus credenciales. 
  
 La separación de las credenciales que se usa durante del lado servidor y las operaciones del lado cliente pueden dar lugar a una incoherencia entre lo que se ve y qué datos se capturan durante una importación o un proceso (una operación del lado servidor). Si las credenciales que está actualmente ha iniciado sesión y las credenciales de suplantación especificadas son diferentes, los datos vea en las características de vista previa y filtrar o **propiedades de la tabla** cuadro de diálogo y los datos capturados durante una importación o proceso puede ser diferente, dependiendo de las credenciales requeridas por el origen de datos.  
  
> [!IMPORTANT]  
>  Al crear un modelo, asegúrese de las credenciales que se ha iniciado sesión y las credenciales especificadas para la suplantación tienen derechos suficientes para capturar los datos del origen de datos.
  
##  <a name="bkmk_imp_info_options"></a> Opciones  
 Al configurar la suplantación, o al editar las propiedades de una conexión de origen de datos existente, especifique una de las siguientes opciones:  
  
**Modelos tabulares 1400 y versiones posteriores**
 
|Opción|Descripción|  
|------------|-----------------|  
|**Suplantar cuenta**|Especifica el modelo usa una cuenta de usuario de Windows para importar o procesar datos desde el origen de datos. El dominio y el nombre de la cuenta de usuario tienen el siguiente formato: **\<nombre de dominio >\\< nombre de la cuenta de usuario\>** .|  
|**Suplantar a usuario actual**|Especifica que deben tener acceso a datos desde el origen de datos mediante la identidad del usuario que envió la solicitud. Esta configuración se aplica solo al modo DirectQuery.|  
|**Suplantar identidad**|Especifica un nombre de usuario para tener acceso a origen de datos, pero no es necesario especificar la contraseña de la cuenta. Esta configuración se aplica solo cuando la delegación Kerberos está habilitada y especifica que se debe usar la autenticación de S4U.|  
|**Suplantar cuenta de servicio**|Especifica el modelo usa las credenciales de seguridad asociadas a la instancia de servicio de Analysis Services que administra el modelo.|  
|**Suplantar cuenta desatendida**|Especifica que el motor de Analysis Services debe usar una cuenta desatendida configurada previamente para tener acceso a los datos.|  

> [!IMPORTANT]
> Suplantar usuario actual no se admite en algunos entornos. Suplantar usuario actual no es compatible con los modelos tabulares implementados en Azure Analysis Services que se conectan a orígenes de datos locales. Dado que un recurso de servidor de Azure Analysis Services no está conectado al dominio de la organización, no se puede autenticar las credenciales del cliente contra un servidor de origen de datos en ese dominio. Azure Analysis Services no actualmente integran también con compatibilidad de la base de datos de SQL (Azure) para el inicio de sesión único (SSO). Dependiendo de su entorno, otras opciones de suplantación también tienen restricciones. Al intentar usar una opción de suplantación que no se admite, se devuelve un error. 


**Modelos tabulares 1200**
 
|Opción|Descripción|  
|------------|-----------------|  
|**Nombre de usuario específico de Windows y contraseña**|Esta opción especifica el modelo usa una cuenta de usuario de Windows para importar o procesar datos desde el origen de datos. El dominio y el nombre de la cuenta de usuario tienen el siguiente formato: **\<nombre de dominio >\\< nombre de la cuenta de usuario\>** . Al crear un modelo nuevo mediante el Asistente para importación de tablas, esta configuración es la opción predeterminada.|  
|**Cuenta de servicio**|Esta opción especifica que el modelo usa las credenciales de seguridad asociadas a la instancia de servicio de Analysis Services que administra el modelo.|  
  
##  <a name="bkmk_impers_sec"></a> Seguridad  
 Las credenciales utilizadas con suplantación son almacena en memoria el motor VertiPaq™. Las credenciales no se escriben nunca en el disco. Si la base de datos del área de trabajo no está en memoria cuando se implementa el modelo, se solicita al usuario que escriba las credenciales usadas para conectarse a los datos de origen de datos y fetch.  
  
> [!NOTE]  
>  Se recomienda especificar una cuenta de usuario y una contraseña de Windows para las credenciales de suplantación. Una cuenta de usuario de Windows puede configurarse para usar privilegios mínimos necesarios para conectarse y leer datos desde el origen de datos.  
  

  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Implementación de soluciones de modelos tabulares](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
