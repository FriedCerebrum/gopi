# GoPI API - Frequently Asked Questions (FAQ)

## General Questions

### Q: What is GoPI API?
A: GoPI API is a service for managing GIF images. It allows you to upload, retrieve, list, and delete GIF files through a simple HTTP API.

### Q: What are the main features?
A: The main features include:
- Uploading GIF files
- Retrieving GIF files by UUID or alias
- Listing all available GIFs
- Deleting GIF files
- Authentication for sensitive operations

### Q: What is the base URL for the API?
A: By default, the API runs on `http://localhost:1111`

## API Endpoints

### Q: What endpoints are available?
A: The API provides four main endpoints:
- `POST /save` - Upload a GIF file
- `GET /gifs` - List all GIFs
- `GET /gif/{id}` - Get a specific GIF
- `DELETE /delete/{id}` - Delete a specific GIF

### Q: Do any endpoints require authentication?
A: Yes, the DELETE endpoint requires basic authentication. Other endpoints are publicly accessible.

## File Upload

### Q: What is the maximum file size for uploads?
A: The maximum file size is 100MB.

### Q: What file formats are supported?
A: Currently, only GIF format is supported. Files must have the `.gif` extension.

### Q: How do I upload a GIF?
A: Use a POST request to `/save` with the file in the form data:
```bash
curl -X POST http://localhost:1111/save -F "file=@path/to/your/file.gif"
```

### Q: What response do I get after uploading?
A: A successful upload returns a JSON response with:
- UUID: unique identifier for the GIF
- Alias: optional friendly name
- Path: storage location

## Retrieving GIFs

### Q: How can I get a list of all GIFs?
A: Send a GET request to `/gifs`:
```bash
curl http://localhost:1111/gifs
```

### Q: How do I retrieve a specific GIF?
A: Use the `/gif/{id}` endpoint with either the UUID or alias:
```bash
curl http://localhost:1111/gif/your-uuid-or-alias
```

## Deleting GIFs

### Q: How do I delete a GIF?
A: Send an authenticated DELETE request:
```bash
curl -X DELETE http://localhost:1111/delete/your-uuid-or-alias -u user:pass
```

### Q: Can deleted GIFs be recovered?
A: No, deletion is permanent and cannot be undone.

## Error Handling

### Q: What are common error responses?
A: Common errors include:
- 400 Bad Request: Invalid file format or size
- 404 Not Found: GIF not found
- 401 Unauthorized: Authentication failed
- 500 Internal Server Error: Server-side issues

### Q: How are errors formatted in responses?
A: Error responses are JSON formatted with status and error message fields:
```json
{
    "status": "error",
    "error": "error description"
}
```

## Best Practices

### Q: What are the recommended practices for using the API?
A: Here are some best practices:
1. Always check file size before uploading
2. Use proper error handling in your code
3. Store UUIDs/aliases for future reference
4. Use secure authentication for delete operations
5. Implement rate limiting in production environments

### Q: Are there any rate limits?
A: The base API implementation doesn't include rate limiting. Consider implementing it based on your needs.
