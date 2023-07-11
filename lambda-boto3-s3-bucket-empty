import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    buckets = s3.list_buckets()
    
    empty_buckets = []
    for bucket in buckets['Buckets']:
        bucket_name = bucket['Name']
        response = s3.list_objects_v2(Bucket=bucket_name)
        if 'Contents' not in response:
            empty_buckets.append(bucket_name)

    if empty_buckets:
        return {
            'noncompliant': True,
            'emptyBuckets': empty_buckets
        }
    else:
        return {
            'noncompliant': False
        }