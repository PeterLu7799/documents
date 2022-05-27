# Progress of creating a shader program

#### Build shaders

```
	- (GLuint)shaderWithName:(NSString*)name type:(GLenum)type {
	  	// Load the shader file
	  	NSString* file;
	  	if (type == GL_VERTEX_SHADER) {
	    	file = [[NSBundle mainBundle] pathForResource:name ofType:@"vsh"];
	  	} else if (type == GL_FRAGMENT_SHADER) {
	    	file = [[NSBundle mainBundle] pathForResource:name ofType:@"fsh"];
	  	}
	  
	  	// Create the shader source
	  	const GLchar* source = (GLchar*)[[NSString stringWithContentsOfFile:file encoding:NSUTF8StringEncoding error:nil] UTF8String];
	  
	  	// Create the shader object
	  	GLuint shaderHandle = glCreateShader(type);
	  
	  	// Load the shader source
	  	glShaderSource(shaderHandle, 1, &source, 0);
	  
	  	// Compile the shader
	  	glCompileShader(shaderHandle);
	  
	  	// Check for errors
	  	GLint compileSuccess;
	  	glGetShaderiv(shaderHandle, GL_COMPILE_STATUS, &compileSuccess);
	  	if (compileSuccess == GL_FALSE) {
	    	GLchar messages[1024];
	    	glGetShaderInfoLog(shaderHandle, sizeof(messages), 0, &messages[0]);
	    	NSLog(@"%@:- GLSL Shader Error: %s", [self class], messages);
	  	}
  
  		return shaderHandle;
	}
```

#### Compile & Link
```
	- (GLuint)programWithVertexShader:(NSString*)vsh fragmentShader:(NSString*)fsh {
	  // Build shaders
	  GLuint vertexShader = [self shaderWithName:vsh type:GL_VERTEX_SHADER];
	  GLuint fragmentShader = [self shaderWithName:fsh type:GL_FRAGMENT_SHADER];
	  
	  // Create program
	  GLuint programHandle = glCreateProgram();
	  
	  // Attach shaders
	  glAttachShader(programHandle, vertexShader);
	  glAttachShader(programHandle, fragmentShader);
	  
	  // Link program
	  glLinkProgram(programHandle);
	  
	  // Check for errors
	  GLint linkSuccess;
	  glGetProgramiv(programHandle, GL_LINK_STATUS, &linkSuccess);
	  if (linkSuccess == GL_FALSE) {
	    GLchar messages[1024];
	    glGetProgramInfoLog(programHandle, sizeof(messages), 0, &messages[0]);
	    NSLog(@"%@:- GLSL Program Error: %s", [self class], messages);
	  }
	  
	  // Delete shaders
	  glDeleteShader(vertexShader);
	  glDeleteShader(fragmentShader);
	  
	  return programHandle;
	}

```

#### Set program and set attributes and uniforms

```
	- (void)vertexShader:(NSString *)vsh fragmentShader:(NSString *)fsh {
	    // Program
	    _program = [self programWithVertexShader:vsh fragmentShader:fsh];
	    
	    // Attributes
	    _aPosition = glGetAttribLocation(_program, "aPosition");
	    
	    // Uniforms
	    _uResolution = glGetUniformLocation(_program, "uResolution");
	    _uTime = glGetUniformLocation(_program, "uTime");
	    
	    // Configure OpenGL ES
	    [self configureOpenGLES];
  	}
  	
  	- (void)configureOpenGLES {
		  // Program
		  glUseProgram(_program);
		  
		  // Attributes
		  glEnableVertexAttribArray(_aPosition);
		  glVertexAttribPointer(_aPosition, 2, GL_FLOAT, GL_FALSE, 0, RWTBaseShaderQuad);
	}
```

#### Render
```
	- (void)renderInRect:(CGRect)rect atTime:(NSTimeInterval)time {
	  // Uniforms
	  glUniform2f(self.uResolution, CGRectGetWidth(rect)*2.f, CGRectGetHeight(rect)*2.f);
	  glUniform1f(self.uTime, time);
	  
	  // Draw
	  glDrawArrays(GL_TRIANGLE_STRIP, 0, 4);
	}
```

#### Vertex shader
```
	// Attributes
	attribute vec2 aPosition;
	
	void main(void) {
	  gl_Position = vec4(aPosition, 0., 1.);
	}
```

#### Fragment shader
```
	// Precision
	precision highp float;

	// Uniforms
	uniform vec2 uResolution;

	void main(void) {

	}
```