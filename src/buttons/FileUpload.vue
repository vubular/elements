<template>
	<b-field class="file" :class="size" v-if="!uploaded && !previous">
        <b-upload v-model="localFile" :loading="!ready" @input="beginUploading">
            <a class="button is-primary" :class="size">
                <span class="icon" v-if="ready"><i class="fa fa-upload"></i></span>
                <span class="icon" v-else><i class="fa fa-spin fa-spinner"></i></span>
                <span> {{'Select file' | translate}} </span>
            </a>
        </b-upload>
        <span class="file-name" v-if="localFile">
            {{ localFile.name }}
        </span>
    </b-field>
    <div v-else>
    	<img v-if="isImage" :src="image" width="50px" />
    	<div v-else v-fawesome="'fal fa-paperclip'"><span>{{localFile.name}}</span></div>
    </div>
</template>
<script>
	export default {
		name: 'FileUploadButton',
		props: {
			previous: String,
			directory: String,
			size: {
				type: String,
				default: 'is-medium'
			}
		},
		data() {
			return {
				file: null,
				ready: true,
				localFile: null,
				uploaded: false
			}
		},
		methods: {
			beginUploading(file) {
				this.ready = false;

				// this.setFileUploadRequest();
				// var apiConfig = Object.assign({}, this.$store.getters['database/config']);

				// var formData = new FormData();
				// formData.append('file', file)

				// this.axios
				// 	.post('https://'+process.env.VUE_APP_ENV_URL+'/upload/'+this.path, formData, apiConfig)
				// 	.then((response) => {
				// 		this.uploaded = true;
				// 		this.file = response.data;
				// 		this.$emit("upload", this.file);
				// 	})
				// 	.then(() => {
				// 		this.ready = true;
				// 		this.setJsonRequest();
				// 	});
			}
		},
		computed: {
			image() {
				if(this.uploaded && this.file) return this.file;
				if(this.previous) return this.previous;
				return null;
			},
			fileName() {
				return (this.file) ? this.file.split("/").pop() : null;
			},
			isImage() {
				return ["jpg","jpeg","png","gif", "svg", "webp"].indexOf(this.exts)!=-1;
			},
			exts() {
				return (this.file) ? this.file.split(".").pop() : null;
			}
		}
	}
</script>