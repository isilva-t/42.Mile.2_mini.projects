# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Makefile                                           :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: isilva-t <isilva-t@student.42porto.com>    +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2024/07/09 16:42:03 by isilva-t          #+#    #+#              #
#    Updated: 2024/07/11 11:23:19 by isilva-t         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

CC = cc
CFLAGS = -Wall -Wextra -Werror

MLX_DIR = ./minilibx-linux/
LIBFT_DIR = ./libs/libft/
LIBFT = ./libs/libft/libft.a

GNL = ./libs/gnl/get_next_line.c \
	./libs/gnl/get_next_line_utils.c
FT_PRINTF = ./libs/ft_printf/ft_printf.c \
	./libs/ft_printf/pf_print_ptr.c \
	./libs/ft_printf/pf_put_nbr_base.c 

MLX = -Lminilibx-linux -lmlx_Linux -Imlx_linux -lXext -lX11 -lm -lz -O3
NAME = fdf

SRCS = $(GNL) ./src/00_fdf.c \
	./src/11_get_map.c \
	./src/12_get_map_utils.c \
	./src/21_get_map_ready_to_show.c \
	./src/22_set_limits.c \
	./src/31_do_mlx_stuff.c \
	./src/32_set_color_based_on_z.c \
	./src/33_draw_line.c \
	./src/34_draw_line_utils.c \
	./src/88_utils.c \
	./src/99_free_stuff.c

OBJS = ${SRCS:.c=.o}
MSG0 = @echo "Compiling..."
MSG1 = @echo "_________________________________________________________________ Compiled ✅"

all: libx $(NAME)

$(NAME):
	$(MSG0);
	@make -C $(MLX_DIR) --silent	
	@make -C $(LIBFT_DIR) --silent
	@$(CC) ${CFLAGS} $(SRCS) $(MLX) $(LIBFT) $(FT_PRINTF) -o $(NAME)
	$(MSG1)

demo:
	./fdf maps/qa_map_tests/16-16.fdf
	
LIBX_DIR = minilibx-linux
libx : $(LIBX_DIR)

.PHONY: libx
.SILENT: $(LIBX_DIR)
$(LIBX_DIR) :
	@if [ ! -d $(LIBX_DIR) ]; then \
		printf "$(YELLOW)Extracting minilibx...$(CLR_RMV)...  "; \
		tar xf minilibx-linux.tgz; \
		printf "$(GREEN)minilibx extracted$(CLR_RMV) ✅\n"; \
	fi
	
.PHONY: rmlibx
rmlibx:
	@if [  -d $(LIBX_DIR) ]; then \
		printf "$(YELLOW)Deleting minilibx...$(CLR_RMV)  "; \
		rm -rf $(LIBX_DIR); \
		printf "$(GREEN)minilibx deleted$(CLR_RMV) ✅\n"; \
	fi

coords: 
	@make -C $(LIBFT_DIR) --silent
	@$(CC) ${CFLAGS} $(SRCS) -D PRINT_COORDS=1 $(MLX) $(LIBFT) $(FT_PRINTF) -o $(NAME)
	$(MSG1)

dimensions: 
	@make -C $(LIBFT_DIR) --silent
	@$(CC) ${CFLAGS} $(SRCS) -D PRINT_DIMENSIONS=1 $(MLX) $(LIBFT) $(FT_PRINTF) -o $(NAME)
	$(MSG1)


clean:
	@make clean -C $(LIBFT_DIR) --silent
	@rm -rf ${OBJS}
	@if [  -d $(LIBX_DIR) ]; then \
	make clean -C $(LIBX_DIR) -s; fi

fclean: clean rmlibx
	@make fclean -C $(LIBFT_DIR) --silent
	@rm -rf ${NAME}

re: fclean all
ret: fclean t
.PHONY: all clean fclean re ret mini mlxdel
