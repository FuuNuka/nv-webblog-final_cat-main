<template>
	<div class="container createcafe box">
		<p class="h1">Edit Cat</p>
		<form v-on:submit.prevent="editCat">
			<label>Cat</label>
			<input type="text" v-model="cat.brand" />
			<label>About</label>
			<p>
				<vue-ckeditor v-model.lazy="cat.about" :config="config" @blur="onBlur($event)"
					@focus="onFocus($event)" />
			</p>

			<label>category</label>
			<input type="text" v-model="cat.category" />
			<label>Price</label>
			<input type="text" v-model="cat.price" />
			<p>
				<button type="submit" class="btn btn-success createuser">update Cat</button>
				<button v-on:click="navigateTo('/cats' )" class="btn btn-warning createuser">กลับ</button>
			</p>
		</form>
	</div>
</template>
<script>
import 'bootstrap/dist/css/bootstrap.min.css'
import CatService from "@/services/CatService";
import VueCkeditor from "vue-ckeditor2";
import UploadService from "@/services/UploadService";
export default {
	data() {
		return {
			cat: {
				brand: "",
				thumbnail: "null",
				pictures: "null",
				about: "",
				category: "",
				price: "",
			},
			config: {
				toolbar: [
					{
						name: "document",
						items: [
							"Source",
							"-",
							"Save",
							"NewPage",
							"Preview",
							"Print",
							"-",
							"Templates",
						],
					},
					{
						name: "clipboard",
						items: [
							"Cut",
							"Copy",
							"Paste",
							"PasteText",
							"PasteFromWord",
							"-",
							"Undo",
							"Redo",
						],
					},
					{
						name: "editing",
						items: ["Find", "Replace", "-", "SelectAll", "-", "Scayt"],
					},
					{
						name: "forms",
						items: [
							"Form",
							"Checkbox",
							"Radio",
							"TextField",
							"Textarea",
							"Select",
							"Button",
							"ImageButton",
							"HiddenField",
						],
					},
					"/",
					{
						name: "basicstyles",
						items: [
							"Bold",
							"Italic",
							"Underline",
							"Strike",
							"Subscript",
							"Superscript",
							"-",
							"CopyFormatting",
							"RemoveFormat",
						],
					},
					{
						name: "paragraph",
						items: [
							"NumberedList",
							"BulletedList",
							"-",
							"Outdent",
							"Indent",
							"-",
							"Blockquote",
							"CreateDiv",
							"-",
							"JustifyLeft",
							"JustifyCenter",
							"JustifyRight",
							"JustifyBlock",
							"-",
							"BidiLtr",
							"BidiRtl",
							"Language",
						],
					},
					{ name: "links", items: ["Link", "Unlink", "Anchor"] },
					{
						name: "insert",
						items: [
							"Image",
							"Flash",
							"Table",
							"HorizontalRule",
							"Smiley",
							"SpecialChar",
							"PageBreak",
							"Iframe",
							"InsertPre",
						],
					},
					"/",
					{ name: "styles", items: ["Styles", "Format", "Font", "FontSize"] },
					{ name: "colors", items: ["TextColor", "BGColor"] },
					{ name: "tools", items: ["Maximize", "ShowBlocks"] },
					{ name: "about", items: ["About"] },
				],
				height: 300
			}
		};
	},
	methods: {
		async editCat() {
			try {
				await CatService.put(this.cat);
				this.$router.push({
					name: "cats",
				});
			} catch (err) {
				console.log(err);
			}
		},
	},
	async created() {
		try {
			let catId = this.$route.params.catId;
			this.catId = (await CatService.show(catId)).data;



		} catch (error) {
			console.log(error);
		}
	},
	components: {
		VueCkeditor
	}
};
</script>
<style scoped>
.dropbox {
	outline: 2px dashed grey;
	/* the dash box */
	outline-offset: -10px;
	background: lemonchiffon;
	color: dimgray;
	padding: 10px 10px;
	min-height: 100px;
	/* minimum height */
	position: relative;
	cursor: pointer;
}

.input-file {
	opacity: 0;
	/* invisible but it's there! */
	width: 100%;
	height: 200px;
	position: absolute;
	cursor: pointer;
}

.dropbox:hover {
	background: khaki;
	/* when mouse over to the drop zone, change color
    */
}

.dropbox p {
	font-size: 1.2em;
	text-align: center;
	padding: 50px 0;
}

ul.pictures {
	list-style: none;
	padding: 0;
	margin: 0;
	float: left;
	padding-top: 10px;
	padding-bottom: 10px;
}

ul.pictures li {
	float: left;
}

ul.pictures li img {
	max-width: 10px;
	margin-right: 20px;
}

.clearfix {
	clear: both;
}

.thumbnail-pic img {
	width: 200px
}

.box {
	padding: 5px;
	border: 2px solid gray;

}

.cafe {
	margin-top: 10px;
}

.createcafe {
	margin: 10px;
	margin-top: 10px;
	margin-left: 100px;
}

input[type=text],
select {
	width: 100%;
	padding: 12px 20px;
	margin: 8px 0;
	display: inline-block;
	border: 1px solid #ccc;
	border-radius: 4px;
	box-sizing: border-box;
}

input[type=password],
select {
	width: 100%;
	padding: 12px 20px;
	margin: 8px 0;
	display: inline-block;
	border: 1px solid #ccc;
	border-radius: 4px;
	box-sizing: border-box;
}

input[type=submit] {
	width: 100%;
	background-color: #4CAF50;
	color: white;
	padding: 14px 20px;
	margin: 8px 0;
	border: none;
	border-radius: 4px;
	cursor: pointer;
}

input[type=submit]:hover {
	background-color: #45a049;
}

div {
	border-radius: 5px;
	background-color: #f2f2f2;
	padding: 20px;
}

label {
	font-size: 20px;
	margin-left: 10px;
}

.createuser {
	margin-top: 20px;
}
</style>
