# 주요 링크
- [S3 버킷 웹사이트 엔드포인트](http://hanghae-assignment-6.s3-website.ap-northeast-2.amazonaws.com)
- [CloudFront 배포 도메인 이름](https://dhtbt5yw2uq37.cloudfront.net)

# CI/CD 구조
![hanghae3 drawio](https://github.com/user-attachments/assets/0ec5ef8c-c2e7-49e4-86ea-f11fd6e042f2)

# 주요 개념
## GitHub Actions과 CI/CD 도구
GitHub Actions는 GitHub 저장소에서 특정 이벤트(예: 코드 푸시) 발생 시 자동으로 작업을 수행하도록 설정할 수 있는 도구입니다. CI/CD(Continuous Integration/Continuous Deployment) 파이프라인을 구축하는 데 사용되며, 코드 변경 사항이 저장소에 푸시될 때마다 프로젝트를 빌드하고 테스트하며, 결과물을 배포할 수 있습니다. 이 이미지에서는 특정 브랜치에 코드가 푸시될 때 GitHub Actions가 실행되어 프로젝트를 빌드하고 그 결과물을 S3 버킷에 업로드합니다.

## S3와 스토리지
AWS S3(Simple Storage Service)는 확장 가능한 객체 스토리지 서비스로, 정적 웹사이트 콘텐츠(HTML, CSS, JavaScript 파일 등)를 저장하고 배포하는 데 사용됩니다. 이 이미지에서는 빌드된 프로젝트 결과물이 S3 버킷에 저장되며, 이 버킷은 CloudFront와 연결되어 있습니다.

## CloudFront와 CDN
AWS CloudFront는 콘텐츠 전송 네트워크(CDN) 서비스로, 전 세계에 분산된 엣지 로케이션을 통해 사용자에게 콘텐츠를 빠르고 안전하게 전달합니다. CloudFront는 S3 버킷의 정적 콘텐츠를 캐싱하여 사용자에게 더 빠른 응답을 제공합니다. 이 이미지에서는 CloudFront가 S3 버킷과 연결되어 있으며, 사용자가 특정 URL로 웹에 접근할 때 CloudFront를 통해 콘텐츠를 전달받습니다.

## 캐시 무효화(Cache Invalidation)
CloudFront는 콘텐츠를 캐싱하여 성능을 향상시키지만, 콘텐츠가 업데이트되었을 때 캐시된 오래된 콘텐츠를 무효화(갱신)해야 합니다. 이는 CloudFront 캐시 무효화(invalidation) 프로세스를 통해 이루어집니다. 이미지에서 CloudFront는 캐시된 콘텐츠가 있는 경우 이를 반환하고, 없는 경우 S3 버킷에서 새로운 콘텐츠를 가져옵니다.

## Repository secret과 환경변수
Repository secret은 GitHub Actions 워크플로우에서 민감한 정보를 안전하게 저장하고 사용하는 방법입니다. 환경변수는 CI/CD 파이프라인에서 다양한 설정 값을 저장하는 데 사용됩니다. GitHub Actions에서 S3에 접근하거나 CloudFront를 관리하기 위해 AWS 자격 증명과 같은 민감한 정보를 Repository secret에 저장하여 사용합니다.
