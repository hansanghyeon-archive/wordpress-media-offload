<p align="center">
<img src="https://user-images.githubusercontent.com/42893446/192394703-9084093c-91a7-4121-b2b5-6f39edb8bbad.jpg" width="250px" style="border-radius: 8px">
</p>


<h2 align="center">Welcome 👋</h2>

> Wordpress & media offload & minio template (docker)

- [Blog Tool, Publishing Platform, and CMS | WordPress.org 한국어](https://ko.wordpress.org/)
- [Upload Your WordPress Media to Amazon S3 with WP Offload Media - Delicious Brains Inc](https://deliciousbrains.com/wp-offload-media/)
- [MinIO | High Performance, Kubernetes Native Object Storage](https://min.io/)

## folder structure

```
.
├── .docker
│   ├── db
│   │   ├── data              // mariadb의 데이터 폴더
│   │   └── .gitkeep
│   ├── minio                 // S3 open source
│   └── wp                    // wordpress:/var/www/html
│       ├── wp-content        // 워드프레스 컨텐츠 폴더
│       └── .gitkeep
├── .env.example
├── .gitignore
├── Makefile
├── README.md
├── apps
│   └── theme                 // 워드프레스에서 사용할 테마 폴더
│       └── .gitkeep
└── docker-compose.yaml
```

## offload media 적용하기

```
// functions
<?php

function minio_s3_client_args( $args ) {
    $args['endpoint'] = 'http://minio:9000';
    $args['use_path_style_endpoint'] = true;
    return $args;
}
add_filter( 'as3cf_aws_s3_client_args', 'minio_s3_client_args' );

add_filter( 'as3cf_aws_s3_url_domain', 'minio_s3_url_domain', 10, 2 );
function minio_s3_url_domain( $domain, $bucket ) {
    return getenv_docker('CDN_DOMAIN', '{{default domain}}').'/' . $bucket;
}
```

```sh
docker-compose up -d
```

## Author

👤 **Hansanghyeon**

* Website: [hyeon.pro](https://hyeon.pro)
* Github: [@Hansanghyeon](https://github.com/Hansanghyeon)
