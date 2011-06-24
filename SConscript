
Import( 'env' )

protobuf_sources = [ 'src/google/protobuf/' + x for x in
        '''stubs/common.cc stubs/once.cc stubs/strutil.cc 
        extension_set.cc 
        generated_message_util.cc message_lite.cc repeated_field.cc 
        wire_format_lite.cc io/coded_stream.cc io/zero_copy_stream.cc
        io/zero_copy_stream_impl_lite.cc '''.split() ]
protobuf = env.Library( 'protobuf', protobuf_sources )

protoc_extra_sources = [ 'src/google/protobuf/' + x for x in
        '''descriptor.cc io/printer.cc unknown_field_set.cc message.cc 
        generated_message_reflection.cc extension_set_heavy.cc
        io/zero_copy_stream_impl.cc reflection_ops.cc descriptor.pb.cc
        descriptor_database.cc io/tokenizer.cc wire_format.cc
        stubs/substitute.cc text_format.cc dynamic_message.cc
        stubs/structurally_valid.cc'''.split() ]

protoc_sources = [ 'src/google/protobuf/compiler/' + x for x in 
        '''code_generator.cc command_line_interface.cc cpp/cpp_enum.cc 
        cpp/cpp_enum_field.cc cpp/cpp_extension.cc cpp/cpp_field.cc  
        cpp/cpp_file.cc cpp/cpp_generator.cc cpp/cpp_helpers.cc
        cpp/cpp_message.cc cpp/cpp_message_field.cc cpp/cpp_primitive_field.cc
        cpp/cpp_service.cc cpp/cpp_string_field.cc java/java_enum.cc 
        java/java_enum_field.cc java/java_extension.cc java/java_field.cc                  
        java/java_file.cc java/java_generator.cc java/java_helpers.cc                
        java/java_message.cc java/java_message_field.cc importer.cc 
        java/java_primitive_field.cc java/java_service.cc parser.cc
        python/python_generator.cc main.cc zip_writer.cc
        java/java_string_field.cc
        plugin.pb.cc subprocess.cc'''.split() ] + protoc_extra_sources
protoc = env.Program( 'protoc', protoc_sources, 
                      LIBS=[protobuf, 'pthread'],
                      CXXFLAGS='-O0 -g0',
                      CPPFLAGS='-DNDEBUG' )

bld = Builder(action = 'libs/protobuf/protoc --cpp_out=src/distmap $SOURCE')
env.Append(BUILDERS = {'ProtocolBufferCompiler' : bld})

result = [protobuf, protoc]
Return( 'result' )



