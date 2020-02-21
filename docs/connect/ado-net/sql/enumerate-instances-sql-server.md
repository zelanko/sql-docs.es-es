---
title: Enumeración de instancias de SQL Server (ADO.NET)
description: Describe cómo enumerar instancias activas de SQL Server.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: d1b5742d082fdb40b03663cf2db719399290a010
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247772"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>Enumeración de instancias de SQL Server (ADO.NET)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server permite que las aplicaciones busquen instancias de SQL Server en la red actual. La clase <xref:System.Data.Sql.SqlDataSourceEnumerator> expone esta información al desarrollador de la aplicación y proporciona un <xref:System.Data.DataTable> que contiene información sobre todos los servidores visibles. Esta tabla devuelta contiene una lista de las instancias de servidor disponibles en la red que coincide con la lista proporcionada cuando un usuario intenta crear una nueva conexión y amplía la lista desplegable que contiene todos los servidores disponibles en el cuadro de diálogo **Propiedades de conexión**. Los resultados mostrados no siempre están completos.  
  
> [!NOTE]
>  Al igual que con la mayoría de los servicios de Windows, es mejor ejecutar el servicio SQL Browser con la cantidad mínima de privilegios posible. Para obtener más información sobre el servicio SQL Browser y cómo administrar su comportamiento, vea los Libros en pantalla de SQL Server.  
  
## <a name="retrieving-an-enumerator-instance"></a>Recuperación de una instancia de enumerador  
Para recuperar la tabla que contiene información sobre las instancias de SQL Server disponibles, primero debe recuperar un enumerador mediante la propiedad <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> compartida o estática:  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
Una vez que haya recuperado la instancia estática, puede llamar al método <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A>, que devuelve un valor <xref:System.Data.DataTable> que contiene información sobre los servidores disponibles:  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
La tabla devuelta por la llamada al método contiene las columnas siguientes, todas las cuales contienen valores `string`:  
  
|Columna|Descripción|  
|------------|-----------------|  
|**ServerName**|Nombre del servidor.|  
|**InstanceName**|Nombre de instancia del servidor. En blanco si el servidor se ejecuta como la instancia predeterminada.|  
|**IsClustered**|Indica si el servidor forma o no parte de un clúster.|  
|**Versión**|Versión del servidor. Por ejemplo:<br /><br /> - 9.00.x (SQL Server 2005)<br />-   10.0.xx (SQL Server 2008)<br />- 10.50.x (SQL Server 2008 R2)<br />-   11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>Limitaciones de enumeración  
Todos los servidores disponibles pueden o no aparecer en una lista. La lista puede variar en función de factores como los tiempos de espera y el tráfico de red. Esto puede hacer que la lista sea diferente en dos llamadas consecutivas. Solo se mostrarán los servidores de la misma red. Los paquetes de difusión no suelen atravesar los enrutadores, por lo que es posible que no vea un servidor en la lista, aunque estará estable en todas las llamadas.  
  
Los servidores listados pueden tener o no información adicional, como `IsClustered` y versión. Esto depende de la forma en que se obtuvo la lista. Los servidores que aparecen en la lista del servicio de explorador de SQL Server tienen más detalles que los que se encuentran a través de la infraestructura de Windows, que solo muestran el nombre.  
  
> [!NOTE]
>  La enumeración de servidores solo está disponible cuando se ejecuta en plena confianza. Los ensamblados que se ejecutan en un entorno de confianza parcial no podrán usarla, aunque tengan el permiso de seguridad de acceso del código (CAS) de <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
SQL Server proporciona información para <xref:System.Data.Sql.SqlDataSourceEnumerator> mediante el uso de un servicio externo de Windows denominado SQL Browser. Este servicio está habilitado de forma predeterminada, pero los administradores pueden desactivarlo o deshabilitarlo, lo que hace que la instancia del servidor sea invisible para esta clase.  
  
## <a name="example"></a>Ejemplo  
La siguiente aplicación de consola recupera información sobre todas las instancias visibles de SQL Server y muestra esa información en la ventana Consola.  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
