# Automatic dependency generation
DEPFLAGS = -MT $@ -MMD -MP -MF $(OBJ_DIR)/$*.d