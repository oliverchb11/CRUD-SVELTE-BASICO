<script>
import {v4} from 'uuid';
import Noty from 'noty';
import 'noty/lib/noty.css';
import 'noty/lib/themes/relax.css';
	let editando = false;
let productos = [
	{
		id:1,
		nombre:'asus gamer',
		descripcion:'computador bueno',
		categoria:'laptops',
		imgUrl:'https://i.linio.com/p/049e62bee973549946479fe399b465ce-zoom.webp'
	},
	{
		id:2,
		nombre:'hp gamer',
		descripcion:'computador super bueno',
		categoria:'laptops',
		imgUrl:'https://i.linio.com/p/049e62bee973549946479fe399b465ce-zoom.webp'
	}
]
	const addProducto = () =>{
		const newProduct = {
			id:v4(),
			nombre:producto.nombre,
			descripcion:producto.descripcion,
			categoria:producto.categoria,
			imgUrl:producto.imgUrl
		}
		productos = productos.concat(newProduct);
		new Noty({
				theme: 'relax',
				type: 'info',
				timeout:3000,
   				text: 'Producto agregado correctamente'
		}).show();
		console.log(productos)
	
		limpiarForm();
	}
	const updateProduct = () =>{
		let updatePro = {
			id:producto.id,
			nombre:producto.nombre,
			descripcion:producto.descripcion,
			categoria:producto.categoria,
			imgUrl:producto.imgUrl
		}

		const productIndex = productos.findIndex(p=>{
			p.id === producto.id
		})
		productos[productIndex] = updatePro;
				new Noty({
				theme: 'relax',
				type: 'success',
				timeout:3000,
   				text: 'Producto actualizado correctamente'
		}).show();
		limpiarForm();
		editando=false
	}
	const editarProducto = (proudctoEdit)=>{
		console.log(proudctoEdit);
		producto = proudctoEdit;
		editando = true;
	}
	const borrarProducto = (id) => {
		
	productos =	productos.filter(producto=>{
				producto.id !== id;
		})
		new Noty({
				theme: 'relax',
				type: 'error',
				timeout:3000,
   				text: 'Producto eliminado correctamente'
		}).show();
	}

	const limpiarForm = () =>{
		producto = {
		id:'',
		nombre:'',
		descripcion:'',
		categoria:'',
		imgUrl:''
		}
	}
	let producto = {
		id:'',
		nombre:'',
		descripcion:'',
		categoria:'',
		imgUrl:''
	};
	const onSubmit = () =>{	
		if(!editando){
			addProducto();
		}else{
			updateProduct();
		}
	}
</script>

<main>

	<div class="container mt-5">
	<h1 class="text-center">Datos del producto</h1>
	<div class="row mt-3">
		
		<div class="col-sm-6">
	<form on:submit|preventDefault={onSubmit}>
		<div class="form-group">
			<input type="text" bind:value={producto.nombre} placeholder="Nombre producto" id="produc-name" class="form-control">
		</div>
		<div class="form-group">
			<input type="url" bind:value={producto.imgUrl} placeholder="www.fazweb.com" id="produc-name" class="form-control" >
		</div>
			<div class="form-group">
			<select class="custom-select" id="category-name" bind:value={producto.categoria}>
			<option selected>Selecione una categoria</option>
			<option value="laptops">laptops</option>
			<option value="perifericos">perifericos</option>
			<option value="servers">servers</option>
			</select>
			</div>
		<div class="form-group">
			<textarea bind:value={producto.descripcion} id="produc-description" placeholder="Descripcion del producto" class="form-control" rows="3"></textarea>
		</div>
		{#if editando === true}
		<button class="btn btn-outline-warning form-control">Editar</button>
		{:else}
		<button class="btn btn-outline-primary form-control">Guardar</button>
		{/if}
	</form>
	</div>
	<div class="col-sm-6">
<table class="table">
  <thead class="thead-dark">
    <tr>
      <th scope="col">nombre</th>
      <th scope="col">categoria</th>
      <th scope="col">descripcion</th>
      <th scope="col">Imagen</th>
      <th scope="col">Editar</th>
      <th scope="col">Borrar</th>
    </tr>
  </thead>
  <tbody>
  	{#each productos as prod}
    <tr >
	<td>{prod.nombre}</td>
      <td>{prod.categoria}</td>
      <td>{prod.descripcion}</td>
	  {#if prod.imgUrl}
	  <td><img src="{prod.imgUrl}" height="50" width="50" alt=""></td>
	  {:else}
      <td><img src="no-img/no-img.png" height="50" width="50" alt=""></td>
	  {/if}
	 

<td>
	<svg width="2em" on:click={editarProducto(prod)} height="2em" viewBox="0 0 16 16" class="bi bi-pencil-square" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
  	<path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456l-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
  	<path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
	</svg>
	  </td>
      <td>
	<svg width="2em" on:click={borrarProducto(prod.id)} height="2em" viewBox="0 0 16 16" class="bi bi-x-octagon-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
 		 <path fill-rule="evenodd" d="M11.46.146A.5.5 0 0 0 11.107 0H4.893a.5.5 0 0 0-.353.146L.146 4.54A.5.5 0 0 0 0 4.893v6.214a.5.5 0 0 0 .146.353l4.394 4.394a.5.5 0 0 0 .353.146h6.214a.5.5 0 0 0 .353-.146l4.394-4.394a.5.5 0 0 0 .146-.353V4.893a.5.5 0 0 0-.146-.353L11.46.146zm.394 4.708a.5.5 0 0 0-.708-.708L8 7.293 4.854 4.146a.5.5 0 1 0-.708.708L7.293 8l-3.147 3.146a.5.5 0 0 0 .708.708L8 8.707l3.146 3.147a.5.5 0 0 0 .708-.708L8.707 8l3.147-3.146z"/>
	</svg>
</td>
	</tr>
	{/each}
  </tbody>
</table>

	</div>
	</div>
	</div>

</main>

<style>

</style>