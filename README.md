# Lab 17 Documentation

### A description of how to use your lambda:
Throughout watching the video demonstrations I tried to follow and apply what I felt was applicable to my lab. Using what I learned in the lab, as well as following the given requests and instructions, I was able to progress only slighly before getting confused as to the direction that the lab was trying to take me. I was able to get some help with Instructor Ryan Gallaway and we were able to get to a point where the lab instructions were making sense. Getting back into the assignment I was able to configure some code to help me progress but ran into some error issues that I couldn't identify. Furthermore I was unable to queue up the logs to find errors. Regardless here is the code I had in progress:


const { S3, S3Client, GetObjectCommand, PutObjectCommand } = require("aws-sdk");

const s3 = new S3();

exports.handler = async (event) => {
    console.log('Event: ', event.Records[0].s3.bucket.name);
    
    const bucketName = event.Records[0].s3.bucket.name;
    
    const key = event.Records[0].s3.object.key;
    
    const fileSize = event.Records[0].s3.object.size;
    
    const type = '.png';
    
    
    let images = await s3.getObject(
        {Bucket: 'd49-jd-images',
         Key: 'images.json'
        }).promise();
    
    try{
        let imageString = images.Body.toString();
        let parseImg = JSON.parse(parseImg);
        
        parseImg.push({
            name: key,
            size: fileSize,
            type
        })
        
    } catch {
        console.log('Error, no file')
    }

    
    
  
    // TODO implement
    const response = {
        statusCode: 200,
        body: JSON.stringify('Hello from Lambda!'),
    };
    return response;
};



    

### A description of any issues you encountered during deployment of this lambda:
Issues that I came across during deployment was understanding (or the lack of) how JSON can be passed through and implemented into the bucket. Another issue I had was syntax related and had to due with how I was wrapping objects and arrays as well as retreiving objects. Other issues I came across had to due with minor things like how I labelled certain variables in relation to the specificity of what trigger I needed, an example would be images being 'JPG' instead of 'jpg', which was creating errors on my end.

### [Image_Link}(https://d49-jd-images.s3.us-west-2.amazonaws.com/Screenshot+(22).png)
